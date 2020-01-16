Source code follows like:

"""Go
for alph := range word { //error

			s3 := alph + s3

		}

"""

then:

cannot range over word (type int)
Go build failed.


so i found some info by googling:

* [[原]可能被忽略的Golang细节——range](https://blog.csdn.net/xingwangc2014/article/details/79777724)

	- range的使用非常简单，对于遍历array，*array，string它返回两个值分别是数据的索引和值，遍历map时返回的两个值分别是key和value，遍历channel时，则只有一个返回数据。

	| range expression | 1st Value | 2nd Value(optional) | notes |
	-----------------------------------------------------
	|string `abcg` | index `int` | rune `int` | 对于string，range迭代的是Unicode而不是字节，所以返回的值是rune |

	"""Go
	func main() {
		for i, c := range "go" {
			fmt.Println(i, c)
		}
	}
	/*
	0 103
	1 111
	*/
	"""


* [Go语言中的byte和rune](https://nanxiao.me/golang-byte-rune/)
	- Go语言中byte和rune实质上就是uint8和int32类型。byte用来强调数据是raw data，而不是数字；而rune用来表示Unicode的code point。