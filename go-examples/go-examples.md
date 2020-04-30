# Go Examples

## How to read/write from/to file in Golang? <a id="titleHolder"></a>

```text
package main
import (
    "io/ioutil"
    "log"
    "fmt"
    "os"
)
func CreateFile() {
    file, err := os.Create("test.txt") // Truncates if file already exists, be careful!
    if err != nil {
        log.Fatalf("failed creating file: %s", err)
    }
    defer file.Close() // Make sure to close the file when you're done
    len, err := file.WriteString("The Go Programming Language, also commonly referred to as Golang, is a general-purpose programming language, developed by a team at Google.")
    if err != nil {
        log.Fatalf("failed writing to file: %s", err)
    }
    fmt.Printf("\nLength: %d bytes", len)
    fmt.Printf("\nFile Name: %s", file.Name())
}
func ReadFile() {
    data, err := ioutil.ReadFile("test.txt")
    if err != nil {
        log.Panicf("failed reading data from file: %s", err)
    }
    fmt.Printf("\nLength: %d bytes", len(data))
    fmt.Printf("\nData: %s", data)
    fmt.Printf("\nError: %v", err)
}
func main() {
    fmt.Printf("########Create a file and Write the content #########\n")
    CreateFile()
    fmt.Printf("\n\n########Read file #########\n")
    ReadFile()
}
```

## Print index and element or data from Array, Slice and Map

```text
package main
import "fmt"
func main() {
    fmt.Println("\n###### Array ######\n")
    intArray := [5]int{1,2,3,4,5}  
    for index,element := range intArray{
        fmt.Println(index,"=>",element)
    }
    fmt.Println("\n###### Slice ######\n")
    intSlice := make([]int,5)
    intSlice[0]=1
    intSlice[1]=2
    intSlice[2]=3
    intSlice[3]=4
    intSlice[4]=5
    for index,element := range intSlice{
        fmt.Println(index,"=>",element)
    }
    fmt.Println("\n###### Map ######\n")
    intStrMap := make(map[string]int)
    intStrMap["A"]=0
    intStrMap["B"]=1
    intStrMap["C"]=2
    intStrMap["D"]=3
    intStrMap["E"]=4
    for index,element := range intStrMap{
        fmt.Println(index,"=>",element)
    }
}
```

{% tabs %}
{% tab title="array" %}
0 =&gt; 1 1 =&gt; 2 2 =&gt; 3 3 =&gt; 4 4 =&gt; 5
{% endtab %}

{% tab title="slice" %}
0 =&gt; 1 1 =&gt; 2 2 =&gt; 3 3 =&gt; 4 4 =&gt; 5
{% endtab %}

{% tab title="map" %}
C =&gt; 2 D =&gt; 3 E =&gt; 4 A =&gt; 0 B =&gt; 1
{% endtab %}
{% endtabs %}

## How to collect information about garbage collection?

Under runtime/debug package function GCStats collects information about recent garbage collections. And PrintStack prints to standard error the stack trace returned by runtime.Stack.

```text
package main
import (
    "flag"
    "fmt"
    "runtime/debug"
)
var (
    garPercent = flag.Int("garC", 50, "Collect information about recent garbage collections")
)
func main() {
    debug.SetGCPercent(*garPercent)
    debug.PrintStack() 
    var garC debug.GCStats
    debug.ReadGCStats(&garC)
    fmt.Printf("\nLastGC:\t%s", garC.LastGC) // time of last collection
    fmt.Printf("\nNumGC:\t%d", garC.NumGC) // number of garbage collections
    fmt.Printf("\nPauseTotal:\t%s", garC.PauseTotal) // total pause for all collections
    fmt.Printf("\nPause:\t%s", garC.Pause) // pause history, most recent first 
}
```

> C:\golang\codes&gt;go run example.go goroutine 1 \[running\]: runtime/debug.Stack\(0x4122b6, 0x2, 0x0\) C:/Go/src/runtime/debug/stack.go:24 +0x64 runtime/debug.PrintStack\(\) C:/Go/src/runtime/debug/stack.go:16 +0x1a main.main\(\) C:/golang/codes/example.go:15 +0x2e
>
> LastGC: 2017-10-29 13:54:12.9605418 +0530 IST NumGC: 1 PauseTotal: 0s Pause: \[0s\] C:\golang\codes&gt;

## How to compare equality of struct, slice and map?

```text
package main
 
import (
"fmt"
"reflect"
)
 
type testStruct struct {
    A int
    B string
    C []int
}
 
func main() {
    st1 := testStruct{A:100,B:"Australia",C:[]int{1,2,3}}   
    st2 := testStruct{A:100,B:"Australia",C:[]int{1,2,3}}
    fmt.Println("Struct equal: ", reflect.DeepEqual(st1, st2))
     
     
    slice1 := []int{1,2,3,4}
    slice2 := []int{1,2,3,4}
    fmt.Println("Slice equal: ", reflect.DeepEqual(slice1, slice2))
     
    map1 := map[string]int{ 
        "x":1,
        "y":2,
    }
    map2 := map[string]int{ 
        "x":1,
        "y":2,
        "z":3,
    }
    fmt.Println("Map equal: ",reflect.DeepEqual(map1, map2))
}
```

## How to reads and decodes JSON values from an input stream?

There are packages like zap, simdjson-go or using a websocket with a codec that is much faster.

```text
package main
 
import (
    "encoding/json"
    "fmt"
    "io"
    "log"
    "strings"
)
 
func main() {
    const jsonStream = `
        {"Name": "John", "City": "Bangkok", "Salary": 54552}        
        {"Name": "Mark", "City": "London", "Salary": 98545}
        {"Name": "Sandy", "City": "Paris", "Salary": 34534}
        {"Name": "Holard", "City": "Tokyo", "Salary": 34534}
    `
    type Employee struct {
        Name, City string
        Salary int32
    }
    dec := json.NewDecoder(strings.NewReader(jsonStream))
    for {
        var emp Employee
        if err := dec.Decode(&emp); err == io.EOF {
            break
        } else if err != nil {
            log.Fatal(err)
        }
        fmt.Printf("%s: %s: %d\n", emp.Name, emp.City, emp.Salary)
    }
}
```

