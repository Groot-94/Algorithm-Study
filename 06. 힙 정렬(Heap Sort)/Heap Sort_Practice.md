## 06. 힙 정렬(Heap Sort)
### 수꿍
- 구현
```swift
private func heapify(_ array: inout [Int], _ givenIndex: Int, _ size: Int) {
    var maxValueIndex = givenIndex
    let leftChildIndex = givenIndex * 2 + 1
    let rightChildIndex = givenIndex * 2 + 2

    if leftChildIndex < size && array[maxValueIndex] < array[leftChildIndex] {
        maxValueIndex = leftChildIndex
    }

    if rightChildIndex < size && array[maxValueIndex] < array[rightChildIndex] {
        maxValueIndex = rightChildIndex
    }

    if maxValueIndex != givenIndex {
        array.swapAt(maxValueIndex, givenIndex)
        heapify(&array, maxValueIndex, size)
    }
}

private func buildHeap(_ array: inout [Int]) {
    var index = array.count / 2

    while index >= 0 {
        heapify(&array, index, array.count)
        index -= 1
    }
}

func heapSort(_ array: inout [Int]) -> [Int] {
    buildHeap(&array)

    var size = array.count
    var index = size - 1

    while index >= 1 {
        array.swapAt(index, 0)

        index -= 1
        size -= 1

        heapify(&array, 0, size)
    }

    return array
}

var array = [521, 13, 22, 25, 1, 999, 3]
print(heapSort(&array))
```
- 설명

```swift
// array의 변경사항을 적용하기 위하여 inout 파라미터 사용
func heapify(_ array: inout [Int], _ givenIndex: Int, _ size: Int) {
    // 최대값이 있는 인덱스를 담아놓기
    var maxValueIndex = givenIndex
    // 좌측 자식 노드의 인덱스
    let leftChildIndex = givenIndex * 2 + 1
    // 우측 자식 노드의 인덱스
    let rightChildIndex = givenIndex * 2 + 2

    // 좌측 노드가 있는지 사이즈를 통해 비교
    // 다음으로, 크기를 비교하여 최대값 최산화
    if leftChildIndex < size && array[maxValueIndex] < array[leftChildIndex] {
        maxValueIndex = leftChildIndex
    }

    // 우측 노드가 있는지 사이즈를 통해 비교
    // 다음으로, 크기를 비교하여 최대값 최산화
    if rightChildIndex < size && array[maxValueIndex] < array[rightChildIndex] {
        maxValueIndex = rightChildIndex
    }

    // 최대값이 있는 인덱스와 기존의 인덱스와 다를 경우 swap
    // 재귀 적용
    if maxValueIndex != givenIndex {
        array.swapAt(maxValueIndex, givenIndex)
        heapify(&array, maxValueIndex, size)
    }
}

func buildHeap(_ array: inout [Int]) {
    // 부모 노드의 인덱스부터 시작하도록 나누기 2
    // 이진 트리 구조에서 자식과 부모의 관계는 2의 배수
    // 좌측 자식 노드는 2의 배수
    // 우측 지식 노드는 2의 배수 + 1 인데
    // 현재 구현부에서는 root를 1이 아닌 0으로 산정하여
    // 좌측: 2의 배수 + 1, 우측: 2의 배수 + 2
    var index = array.count / 2

    // root까지 heapify 반복
    while index >= 0 {
        heapify(&array, index, array.count)
        index -= 1
    }
}

// 위의 과정까지가 힙 구조를 만드는 과정
// 여기부터 힙 정렬
func heapSort(_ array: inout [Int]) -> [Int] {
    // 힙 구조 만들기
    buildHeap(&array)

    var size = array.count
    var index = size - 1

    // index는 0이 가장 낮은 값이기 때문에
    // 내부 while문에서 index를 1씩 빼주고 있으니
    // 0번째와 0번째는 굳이 swap이 불필요하므로
    // index가 1이상일 경우만 반복
    while index >= 1 {
        // 가장 큰 값이 root에 있으니
        // 이를 맨 마지막 인덱스와 swap
        array.swapAt(index, 0)

        // 이제 다음 인덱스로 넘어감
        index -= 1
        // 사이즈를 줄이는 이유는
        // 맨 마지막에 들어갈 값을 알았으니
        // removeLast로 대체 가능
        size -= 1

        // 또다시 max가 root로 가도록 메서드 적용
        heapify(&array, 0, size)
    }

    return array
}

// 정렬이 잘 되는지 확인
// let이 아닌 var로 사용한 이유는 inout 때문
var array = [521, 13, 22, 25, 1, 999, 3]
print(heapSort(&array))

```

### Judy
```swift
func heapSort(_ array: [Int]) -> [Int] {
    var arr = array
    
    for i in stride(from: array.count - 1, to: -1, by: -1) {
        arr = makeMaxHeap(arr, i)	// 이미 정렬된 부분은 빼고 최대 힙으로 구성
        arr.swapAt(0, i)	// 마지막 노드와 루트 노드를 swap -> 가장 큰수를 마지막으로
    }
    
    return arr
}

// 최대 힙으로 만드는 함수
func makeMaxHeap(_ array: [Int], _ maxIndex: Int) -> [Int] {
    var arr = array
    
    for j in stride(from: maxIndex, to: 0, by: -1) { // 마지막 노드부터 비교 
        if arr[j] > arr[(j-1)/2] {	// 부모 노드와 비교
            arr.swapAt(j, (j-1)/2)	// 부모 노드보다 크면 swap
        }
    }
    
    return arr
}
```

### Yeton
```swift
func myMaxHeapSort(_ array: [Int]) -> [Int] {
    var newArray = array
    
    for i in stride(from: array.count - 1, to: -1, by: -1) {
        newArray = makeMaxHeap(newArray, i)
        newArray.swapAt(0, i)
    }
    
    return newArray
}

func makeMaxHeap(_ array: [Int], _ maxIndex: Int) -> [Int] {
    var newArray = array
    
    for j in stride(from: maxIndex, to: 0, by: -1) {
        if j % 2 == 0 {
            if newArray[j] > newArray[(j-1)/2] {
                newArray.swapAt(j, (j-1)/2)
            }
        } else {
            if newArray[j] > newArray[j/2] {
                newArray.swapAt(j, j/2)
            }
        }
    }
    
    return newArray
}

myMaxHeapSort([1,5,20,14,7,6,30])
```

### Groot
```swift
func heapSort(_ value: [Int]) -> [Int] {
    var result = value
    
    for index in stride(from: result.count - 1, through: 0, by: -1) { // MaxHeap을 구성하기 위해서 루트(0) 값이 가장 커야하기 때문에 배열의 뒤에서(heap의 가장 아래부분)부터 반복시작
        result = makeMaxHeap(result, index) // MaxHeap을 만들어줌
        result.swapAt(0, index) // root를 마지막 노드로 교체
    }
    
    return result
}

func makeMaxHeap(_ value: [Int], _ maxIndex: Int) -> [Int] {
    var result = value
    
    for index in stride(from: maxIndex, to: 0, by: -1) { // 밑에서부터 부모의 값보다 자식의 값이 크면 변경
            if result[index] > result[index/2] {
                result.swapAt(index, index/2)
            }
        }
    
    return result
}
```
