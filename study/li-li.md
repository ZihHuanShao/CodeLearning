# Error handling \(錯誤處理\)範例

```swift
// 錯誤處理必須遵從Error協定
enum NameInputError:Error{
    case empty
    case isNumber
}

func getUserFullname(firstname:String, lastname:String) throws -> String{
    if firstname == "" || lastname == ""{
        throw NameInputError.empty
    }else if Int(firstname) != nil || Int(lastname) != nil{
        throw NameInputError.isNumber
    }
    
    let fullname = firstname + " " + lastname
    return fullname
}

do{
    try getUserFullname(firstname: "Thomas", lastname: "Lee")
}catch NameInputError.empty{
    print("empty name")
}catch NameInputError.isNumber{
    print("input some number")
}catch{
    print("something wrong")
}


```

