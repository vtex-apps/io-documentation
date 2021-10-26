# Properties 

Every JSON is defined between `{ }` by keys and values that together define its properties i.e. its **inherent characteristics**. 

```json
{
 "name": "Pedro",
 "height": 1.90
}
```

In the example above, `name` and `height` are the object's keys whose values are, respectively, `Pedro` and `1.90`. 

The `key + value` set constitutes what we call the property (or *prop*) of the JSON, being responsible for qualifying it by setting its essential characteristics.

>ℹ️ The key and value can also be called, respectively, property name and property value.

In the blocks context, the properties (`props`) end up acting on the **definition of the performance and visual identity of the component rendered in the interface** - the more props a block has, the more flexible its configuration is for the end user.

The list of properties a JSON accepts are separated by comma (`,`), and the values can vary according to their type:

- `string` - A prop of the `string` type has its value in quotation marks, being a text composed by alphabetic characters.
- `number` - A prop of the type `number` has its value without quotation marks, being it an integral or real number. When it is the real type, the `.` (dot) character should be used to separate the integral part from the decimal places. E.g.: `1` (integer) or `23.454` (real).
- `boolean` - A prop of the `boolean` type has its value without quotes, being necessarily `true` or `false`.
- `object` - A prop of the 'object' type has its value between curly brackets `{}` being a list with various data types, that is, a new object. 
- `array` - A prop of the `array` type has its value between brackets `[]`, being a list with only one data type.

There are two other types also used by the Store Framework blocks properties:

- `enum` - A prop of the `enum` type has its value between quotation marks and predefined by the React component to which the correspondent block.
- `block` - A prop of the type `block` has its value quotes, being it the name of a block and its app's version. This property will be responsible for rendering the block as its value. E.g.: `icon-cart` (from the [Store Icons](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-icons) app).
