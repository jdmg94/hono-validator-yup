# Yup validator middleware for Hono

The validator middleware using [Yup](https://github.com/jquense/yup) for [Hono](https://honojs.dev) applications.
You can write a schema with Yup and validate the incoming values.

## Usage

```ts
import * as yup from "yup";
import { yValidator } from "hono-validator-yup";

const schema = yup.object().shape({
  name: yup.string(),
  age: yup.number(),
});

app.post("/author", yValidator("json", schema), (c) => {
  const data = c.req.valid("json");
  return c.json({
    success: true,
    message: `${data.name} is ${data.age}`,
  });
});
```

Hook:

```ts
app.post(
  "/post",
  yValidator("json", schema, (result, c) => {
    if (!result.success) {
      return c.text("Invalid!", 400);
    }
  })
  //...
);
```

## Author

José Muñoz <https://github.com/jdmg94>

## License

MIT
