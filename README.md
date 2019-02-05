# 试验GraphQL

# 试验

修改```GraphQLDataFetchers```中静态数据的内容，改所有id为纯数字。  
发送```POST```请求到```/graphql```，请求头中有```Content-Type```为```application/json```，
请求数据
```
{
    "query": "{
                  bookById(id: '1'){
                      id
                      name
                      pageCount
                      author {
                          firstName
                          lastName
                      }
                  }
              }"
}
```
发送GET请求到```/graphql```，加上查询```?query=略```

# 初步探索
见```graphql.spring.web.servlet.components.GraphQLController```类，
其中可见```@RequestMapping(value = "${graphql.url:graphql}"```。
若是POST，将body转换为```graphql.spring.web.servlet.components.GraphQLRequestBody```类，其中有属性```String query```，```String operationName```，```Map<String, Object> variables```；
若是GET，查询字符转必需有```query```，可选```operationName```，```variables```。

# 踩坑

官网[spring-boot](https://www.graphql-java.com/tutorials/getting-started-with-spring-boot/)上的例子，
有错误
其中```ID```类型只能为数字，教程中```book-1```报错
```
{
  "errors": [
    {
      "message": "Validation error of type WrongType: argument 'id' with value 'EnumValue{name='book1'}' is not a valid 'ID' @ 'bookById'",
      "locations": [
        {
          "line": 1,
          "column": 11
        }
      ]
    }
  ]
}
```
若将```ID```换为字符串```'1'```或数字```1```均可成功
