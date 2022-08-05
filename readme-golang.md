1.

    vagrant@server1:~$ go version
    go version go1.13.8 linux/amd64

2. Check

3.

    package main
      import "fmt"
      func main() {
        var foot float64
          fmt.Print("Type foot: ")
          fmt.Scanf("%f", &foot)           
          result := foot * 0.3048 
          fmt.Println("Meters:", result )
            }
    
    
    vagrant@server1:~/golang$ go run script1.go
    Type foot: 10
    Meters: 3.048

4.

    package main
      import "fmt"
      func main() {
        x := []int{48,2, 96,86,3,68,57,82,63,70,37,34,83,27,19,97,9,17}
        min := 0
        for i, less := range x {
          if (i == 0) {
            min = less
          } else {
            if (less < min) {
              min = less
            }
          }
          }
        fmt.Println("Min integer: ", min)
      }
      
    vagrant@server1:~/golang$ go run script2.go
    Min integer:  2

5.

    package main
      import "fmt"
       func main() {
        for i := 1; i <= 100; i++ {
          if (i%3) == 0 {
            fmt.Print("[",i,"]")
          }
        }
      }
      
    vagrant@server1:~/golang$ go run script3.go
    [3][6][9][12][15][18][21][24][27][30][33][36][39][42][45][48][51][54][57][60][63][66][69][72][75][78][81][84][87][90][93][96][99]
