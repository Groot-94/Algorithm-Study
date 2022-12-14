### ๐ ๋ณํฉ ์ ๋ ฌ(Merge Sort)
- ๋น๊ต ๊ธฐ๋ฐ ์ ๋ ฌ ์๊ณ ๋ฆฌ์ฆ.
- ์์ด์ ํ๋์ ์๊ฐ ๋  ๋๊น์ง ๋ถํ ์ ํ ํ ๋ค์ ๋ณํฉํ๋ ์ ๋ ฌ ๋ฐฉ์์ด๋ค.

![](https://i.imgur.com/Clav1zC.gif)

#### ๐ ๊ตฌํ๋ฐฉ๋ฒ
1. ๋ฆฌ์คํธ์ ๊ธธ์ด๊ฐ 1 ์ดํ๋ผ๋ฉด ์ด๋ฏธ ์ ๋ ฌ๋ ๊ฒ์ผ๋ก ๋ณธ๋ค.
2. ๋ถํ (divide): ์ ๋ ฌ๋์ง ์์ ๋ฆฌ์คํธ๋ฅผ ์ ๋ฐ์ผ๋ก ์๋ผ ๋น์ทํ ํฌ๊ธฐ์ ๋ ๋ถ๋ถ ๋ฆฌ์คํธ๋ก ๋๋๋ค.
3. ์ ๋ณต(conquer): ๊ฐ ๋ถ๋ถ ๋ฆฌ์คํธ๋ฅผ ์ฌ๊ท์ ์ผ๋ก ํฉ๋ณ ์ ๋ ฌ์ ์ด์ฉํด ์ ๋ ฌํ๋ค.
4. ๊ฒฐํฉ(combine): ๋ ๋ถ๋ถ ๋ฆฌ์คํธ๋ฅผ ๋ค์ ํ๋์ ์ ๋ ฌ๋ ๋ฆฌ์คํธ๋ก ํฉ๋ณํ๋ค. ์ด๋ ์ ๋ ฌ ๊ฒฐ๊ณผ๊ฐ ์์๋ฐฐ์ด์ ์ ์ฅ๋๋ค. <- ์ค์  ์ ๋ ฌ์ด ์ด๋ค์ง๋ ๊ตฌ๊ฐ.
5. ๋ณต์ฌ(copy): ์์ ๋ฐฐ์ด์ ์ ์ฅ๋ ๊ฒฐ๊ณผ๋ฅผ ์๋ ๋ฐฐ์ด์ ๋ณต์ฌํ๋ค.

![](https://i.imgur.com/z3At868.png)

#### ๐ ์ฅ๋จ์ 
- ์ฅ์ 
    - input์ ์ ๋ ฌ ์ ๋์ ๊ด๋ จ์์ด ์ด๋ ์ ๋์ ์ฑ๋ฅ์ ๋ณด์ฅํด์ค๋ค.
- ๋จ์ 
    - ์ด๋ฏธ ์ ๋ ฌ๋์ด ์๋ Input์ด๋ผ๋ ํญ์ ๊ฐ์ ํ์์ ์ฐ์ฐ์ ํ๋ค.
    - ๋ณ๋์ ์์ ๋ฐฐ์ด์ด ํ์ํ๋ค.(์ ์๋ฆฌ ์ ๋ ฌ = in-place sorting)์ด ์๋๋ค.
    - ์ถ๊ฐ์ ์ธ Memory๊ฐ ํ์ํ๋ค.

#### ๐ ์๊ฐ๋ณต์ก๋ 
- ์ต์ ์๊ฐ๋ณต์ก๋ O(n log n)
- ์ต์  ์๊ฐ๋ณต์ก๋ O(n log n)
- ํ๊ท  ์๊ฐ๋ณต์ก๋ ์ผ๋ฐ์ ์ผ๋ก, O(n log n)
- ๊ณต๊ฐ๋ณต์ก๋	ะ(n)

#### ๐ ์ฝ๋
```swift
import Foundation

func mergeSort(_ value: [Int]) -> [Int] {
    guard value.count > 1 else { return value }
    
    let mid = value.count / 2
    let left = Array(value[0..<mid])
    let right = Array(value[mid..<value.count])
    
    return merge(mergeSort(left), mergeSort(right))
}

func merge(_ left: [Int], _ right: [Int]) -> [Int] {
    var left = left
    var right = right
    var result = [Int]()
    
    while !left.isEmpty && !right.isEmpty { // ๋ ๋ค ์ซ์๋ฅผ ๊ฐ์ง๊ณ  ์์ ๋
        if left.first! < right.first! { // ๋ ์์ ๊ฐ์ ์์๋๋ก ๋ฃ์ด์ค๋ค.
            result.append(left.removeFirst())
        }else {
            result.append(right.removeFirst())
        }
    }
    
    result.append(contentsOf: left+right) // ๋จ์ ์ซ์๋ค์ ์ถ๊ฐํด์ค๋ค.
    
    return result
}
```
https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC
https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html
https://babbab2.tistory.com/102
