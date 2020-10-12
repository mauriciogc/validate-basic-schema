# View all rules [json-schema.org](https://json-schema.org/understanding-json-schema/reference/index.html)

## JSON Schemas with @cfworker/json-schema

Copy & paste in index.js to see demo

---

## Numbers

### Basic

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "number",
};

const data = 100;

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### multipleOf

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "number",
	multipleOf: 10,
};

const data = 50;

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### range

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "number",
	minimum: 33,
};

const data = 34;

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

---

## String

### string

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "string",
};

const data = "mauricio";

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### length

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "string",
	minLength: 2,
	maxLength: 3,
};

const data = "mau";

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### format

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "string",
	format: "date",
};

const data = "2020-31-01";

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### pattern

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "string",
	pattern: "^(\\([0-9]{3}\\))?[0-9]{3}-[0-9]{4}$",
};

const data = "555-1234";

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

---

## Boolean

### boolean

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "boolean",
};

const data = false;

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

---

## Null

### null

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "boolean",
};

const data = false;

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

---

## Object

### object

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "object",
};

const data = {
	key: "value",
	another_key: "value_2",
};

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### properties

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "object",
	properties: {
		name: { type: "string" },
		lastName: { type: "string" },
		address: {
			type: "object",
			properties: {
				country: { type: "string" },
				city: { type: "string" },
			},
		},
		age: { type: "integer" },
	},
};

const data = {
	name: "Mauricio",
	lastName: "García",
	address: {
		country: "México",
		city: "CDMX",
	},
	age: 37,
};

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### aditional properties

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "object",
	properties: {
		name: { type: "string" },
		lastName: { type: "string" },
		address: {
			type: "object",
			properties: {
				country: { type: "string" },
				city: { type: "string" },
			},
			additionalProperties: true,
		},
		age: { type: "integer" },
	},
	additionalProperties: false,
};

const data = {
	name: "Mauricio",
	lastName: "García",
	address: {
		country: "México",
		city: "CDMX",
		cp: "03100",
	},
	age: 37,
};

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### required

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "object",
	properties: {
		name: { type: "string" },
		lastName: { type: "string" },
		address: {
			type: "object",
			properties: {
				country: { type: "string" },
				city: { type: "string" },
			},
			additionalProperties: true,
			required: ["country"],
		},
		age: { type: "integer" },
	},
	additionalProperties: false,
	required: ["name", "lastName", "address", "age"],
};

const data = {
	name: "Mauricio",
	lastName: "García",
	address: {
		country: "México",
		cp: "03100",
	},
	age: 37,
};

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### Size

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "object",
	minProperties: 2,
	maxProperties: 4,
	properties: {
		name: { type: "string" },
		lastName: { type: "string" },
		address: {
			type: "object",
			properties: {
				country: { type: "string" },
				city: { type: "string" },
			},
			additionalProperties: true,
			required: ["country"],
		},
		age: { type: "integer" },
	},
	additionalProperties: true,
	required: ["name", "lastName"],
};

const data = {
	name: "Mauricio",
	lastName: "García",
	address: {
		country: "México",
		cp: "03100",
	},
	age: 37,
};

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### Dependencies

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "object",
	minProperties: 2,
	maxProperties: 4,
	properties: {
		name: { type: "string" },
		lastName: { type: "string" },
		address: {
			type: "object",
			properties: {
				country: { type: "string" },
				city: { type: "string" },
			},
			additionalProperties: true,
			required: ["country"],
		},
		age: { type: "integer" },
	},
	additionalProperties: true,
	required: ["name", "address"],
	dependencies: {
		name: ["lastName"],
		lastName: ["name"],
	},
};

const data = {
	name: "Mauricio",
	lastName: "García",
	address: {
		country: "México",
		cp: "03100",
	},
	age: 37,
};

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

---

## Array

### Array

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "array",
};

const data = ["Mauricio", 37, true, { address: { country: "México" } }];

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### items

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "array",
	items: {
		type: "number",
	},
};

const data = [1, 2, 3, 4];

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### contains

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "array",
	contains: {
		type: "number",
	},
};

const data = ["Mauricio", "García", 37];

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### tuple validaton

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "array",
	items: [
		{ type: "string" },
		{ type: "string" },
		{
			type: "object",
			properties: {
				address: {
					type: "object",
					properties: {
						country: {
							type: "string",
						},
					},
					required: ["country"],
				},
			},
			required: ["address"],
		},
		{ type: "number" },
	],
};

const data = ["Mauricio", "García", { address: { country: "CDMX" } }, 37];

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### size

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "array",
	minItems: 2,
	maxItems: 3,
};

const data = ["Mauricio", "García"];

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

---

## Enum

### enum

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "number",
	enum: [1, 2, 3, 4, 5],
};

const data = 6;

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

---

## Constant values

### const

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "object",
	properties: {
		name: { type: "string" },
		lastName: { type: "string" },
		address: {
			type: "object",
			properties: {
				country: { type: "string", const: "México" },
				city: { type: "string" },
			},
			additionalProperties: true,
			required: ["country"],
		},
		age: { type: "integer" },
	},
	additionalProperties: true,
	required: ["name", "address"],
};

const data = {
	name: "Mauricio",
	lastName: "García",
	address: {
		country: "México",
		cp: "03100",
	},
	age: 37,
};

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

---

## Combining schemas

### anyOf

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	anyOf: [{ type: "string" }, { type: "number" }],
};

const data = 6;

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

### oneOf

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	oneOf: [
		{ type: "number", multipleOf: 5 },
		{ type: "number", multipleOf: 3 },
	],
};

const data = 6;

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

---

## Conditionals

### if, then, else

```javascript
import { Validator } from "@cfworker/json-schema";

const schema = {
	type: "object",
	properties: {
		name: "string",
		age: "number",
		address: {
			type: "object",
			properties: {
				country: {
					enum: ["México", "Canada"],
				},
			},
			if: {
				properties: { country: { const: "México" } },
			},
			then: {
				properties: { postal_code: { pattern: "[0-9]{5}(-[0-9]{4})?" } },
			},
			else: {
				properties: {
					postal_code: { pattern: "[A-Z][0-9][A-Z] [0-9][A-Z][0-9]" },
				},
			},
		},
	},
};

const data = {
	name: "Mauricio",
	lastName: "García",
	address: {
		country: "Canada",
		postal_code: "K1M 1M4",
	},
	age: 37,
};

const validator = new Validator(schema);
const result = validator.validate(data);

console.log("==>", result);
```

---

## Generic Keywords

### $schema, title, description, $comment, examples

```javascript
const schema = {
	$schema: "http://json-schema.org/draft-07/schema#",
	title: "My schema title",
	description: "A short description",
	$comment: "This its a comment",
};
```
