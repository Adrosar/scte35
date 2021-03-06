# scte35			[![Go Report Card](https://goreportcard.com/badge/github.com/FUTZU/scte35)](https://goreportcard.com/report/github.com/FUTZU/scte35)
The SCTE 35 Parser in Go.
### Heads up, work in progress.

#### What is working:
✓ Parsing MPEG-TS files

✓ Parsing Base64 strings

✓ Splice Info Section 	
	
✓ Splice Null
	
✓ Time Signal
	
✓ Splice Insert   	 	
	
✓ Bandwidth Reservation
	
✓ Private Command		

#### Installation
```sh
go get -u github.com/futzu/scte35
```

#### Parsing local MPEG-TS files

```go
/** call this file test.go
	
    go build test.go
	
  ./test video1 video2 video3
**/ 	
package main

import (
	"os"
	"fmt"
	"github.com/futzu/scte35"
)

func main(){

	args := os.Args[1:]
	for i := range args{
		fmt.Printf( "\nNext File: %s\n\n",args[i] )
		scte35.FileParser(args[i])
	}
}     
```

#### Parsing a base64 string
```go
/** call this file test1.go

    go build test1.go 
    
   ./test1 "/DAvAAAAAAAA///wFAVIAACPf+/+c2nALv4AUsz1AAAAAAAKAAhDVUVJAAABNWLbowo="
**/

package main

import (
	"os"
	"fmt"
	"github.com/futzu/scte35"
)

func main() {


	args := os.Args[1:]
	for i := range args{
		bites := scte35.DeB64(args[i])
		fmt.Println(args[i])
		scte35.SCTE35Parser(bites)
	}
}
```  
---
##### Output
```sh
{Name:Splice Info Section TableId:0xfc SectionSyntaxIndicator:false
Private:false Reserved:0x3 SectionLength:47 ProtocolVersion:0
EncryptedPacket:false EncryptionAlgorithm:0 PtsAdjustment:0 CwIndex:0xff 
Tier:0xfff SpliceCommandLength:20 SpliceCommandType:5}
{Name:Splice Insert SpliceEventId:0x4800008f SpliceEventCancelIndicator:false 
OutOfNetworkIndicator:true ProgramSpliceFlag:true DurationFlag:true BreakAutoReturn:true 
BreakDuration:60.293566 SpliceImmediateFlag:false TimeSpecifiedFlag:true PTS:21514.559088 
ComponentCount:0 Components:[] UniqueProgramId:0 AvailNum:0 AvailExpected:0 Identifier:0}

```

