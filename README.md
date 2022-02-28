**Variable**: Variablename or #"Variable name"

```
let
    Variablename = expression,
    #"Variable name" = expression2
in
    #"Variable name"
```

**Comment**: //

**Primitive value**: number, logical (true false), text, null

**List**: {1, 2, 3}, {123, true, "A"}, {1..5} is 1, 2, 3, 4, 5, the same {a..z}

**Fields**: a name/value pair. Name is text that unique in record. A = 1

**Record**: a set of *fields*. 

- ```
  [
      A = 1,
      B = 2,
      C = 3
  ]
  ```

**Table**: a set of *columns* (are identified by name) and *rows*

- ```
  #table({"col1", "col2"}, { {1, 2}, {3, 4} })
  col1    col2
  1        2
  3        4
  ```

**Function**: invoke argument and produce value is followed `=>`

- ```
  (x, y) => (x+y)/2
  ex: (4, 2) => (4+2)/2 = 3
  [
      Add = (x, y) => x + y,
      A = Add(1, 1),    //2
      B = Add(A, 5)     //7
  ]
  ```

**Evaluation**: can use record 

- ```
  [
      A1 = A2 * 2,
      A2 = A3 + 1,
      A3 = 1
  ]
  //The above expression is equivalent 
  [
      A1 = 4,
      A2 = 2,
      A3 = 1
  ]
  ```

- Record can be nest in other records. Can use the *lookup operator* `[]` to access field of record by name
  
  ```
  [
      Sales = [ First = 1000, Second = 1500],
      Total = Sales[First] + Sales[Second]
  ]
  //The above expression is equivalent 
  [
      Sales = [ First = 1000, Second = 1500],
      Total = 2500
  ]
  ```

- Use the *positional index operator* `{}` in list, begin from `0`
  
  ```
  [
      Test = 
          {
              [
                  A = 10,
                  B = 20,
                  C = A + B //30
              ],
              [
                  A = 1,
                  B = 2,
                  C = A + B //3
              ]
          },
      Test2 = Test{0}[C] + Test{1}[C]    //33
  ]
  ```





**Library**:

- Table.TransfromColumns(table, {"Column name", Text.Proper}): capital text

- ```
  Number.E    //e = 2.7182...
  Text.PositionOf("Hello", "ll") //2
  ```

- 



**Operators**:

- `+`
  
  ```
  1 + 2    //3
  #time(12, 23, 0) + #duration(0, 0, 2, 0)    //#time(12, 25, 0)
  1 + "2"    // error: add number and text
  ```

- `&`: combine
  
  ```
  "A" & "BC"    //"ABC"
  {1} & {2, 3}    //list concatenation: {1, 2, 3}
  [ a = 1 ] & [ b = 2 ]    //record merge: [ a = 1, b = 2 ]
  ```

- 



**Metadata**: a record that store metadata for a value (nhiều kiểu data khác nhau)

- Syntax: a metadata record value `y` associate with a exist value `x` is
  
   `x meta y`
  
  ```
  "A" meta [ A1 = 5, A2 = {"m", "n"} ]
  ```

- Merge metadata
  
  ```
  ("A" meta [ A1 = 5 ]) meta [ A2 = {"m", "n"} ]
  //is equivalent
  "A" meta ([ A1 = 5 ] & [ A2 = {"m", "n"} ])
  ```

- Access value of metadata record by `Value.Metadata` function
  
  ```
  [ 
      X = "A" meta [ A1 = 5, A2 = {"m"} ], 
      XAccess = Value.Metadata(X)[A1]    //5
  ]
  ```

- 

**Let expression**: The **let** expression allows a set of values to be computed, assigned names, and then used in a subsequent expression that follows the **in**

- ```
  let
      A = [ B = 1, C = 2 ],
      X = [ Y = 3, Z = 4 ]
  in
      A[B] + X[Y]    //1 + 3 = 4
  ```

- 



**If expression**: base on logical condition

- ```
  if 2 > 1 then
      2 + 2
  else
      1 + 1
  ```

- 
