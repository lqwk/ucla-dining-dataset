# UCLA Dining Hall Menus Dataset

Menu data downloaded from the UCLA dining hall website from **July 25, 2016** to **April 10, 2017**.

# Dataset Structure

The dataset is included within the `data` subdirectory and is separated into versions `v1` and `v2` (more details below).

## Readability

The data is in a compact JSON form so it would be a good idea to run it through a JSON beautifier for readability. In fact Python comes with a built-in tool that accomplishes this.

```shell
$ python -m json.tool <JSON-FILE>
```

## Versions & Structure

The two versions have different structures, which is derived from the UCLA dining hall website. Details of each version can be found below.

### Top level

Dictionary of 3 elements looking similar to the following:

```js
{
  "b": [],  // breakfast
  "l": [],  // lunch
  "d": []   // idnner
}
```

where each element is an array containing data for each `meal`.

### `meal` Array, `restaurant` Dictionary

In the `meal` arrays, there are a list of `restaurant` dictionaries that contain two elements shown below:

```js
{
  "r": "...",  // restaurant name
  "rk": []     // restaurant kitchens
}
```

in which each `restaurant` contains a `restaurant kitchen` array that contains a list of `kitchen` dictionaries.

### `kitchen` Dictionary

A `kitchen` dictionary has the structure similar to the following:

```js
{
  "k": "...",  // kitchen name
  "i": []      // kitchen items
}
```

in which each `kitchen` contains a `kitchen items` array that contains a list of `item` dictionaries.

### `item` Dictionary

Each `item` has the following structure:

```js
{
  "e": "...", // entree name
  "t": "...", // entree type
  "n": []     // nutrition information
}
```

Nutrition information and `type` information will be further explained in the sections below.

#### Nutrition Information

The nutrition information array has the following structure, with the array `index` (0-based index) and type of nutrition information in the comments.

```js
[
  "0",   // 0, total calories
  "0",   // 1, calories from fat

  "0%",  // 2,  vitamin A
  "0%",  // 3,  vitamin C
  "0%",  // 4,  calcium
  "0%",  // 5,  iron

  "0g",  // 6,  total fat
  "0%",  // 7,  total fat percentage
  "0g",  // 8,  saturated fat
  "0%",  // 9,  saturated fat percentage
  "0g",  // 10, trans fat

  "0mg", // 11, cholesterol
  "0%",  // 12, cholesterol percentage
  "0mg", // 13, sodium
  "0%",  // 14, sodium percentage

  "0g",  // 15, total carbohydrate
  "0%",  // 16, total carbohydrate percentage
  "0g",  // 17, dietary fiber
  "0%",  // 18, dietary fiber percentage
  "0g",  // 19, sugars

  "0g"   // 20, protein
]
```

#### `type` Information

Key Difference Between `v1` and `v2`: `v2` contains more information (not just vegetarian or vegan) on what the entree contains (dairy, soy, seafood, etc.)

Details on each version can be found below.

##### Version `v1`

`type` information is a single character string which shows that the entree is one of the following types:

| Key String | Type Information |
| ---------: | ---------------- |
|        `o` | Ordinary         |
|        `v` | Vegetarian       |
|        `g` | Vegan            |

##### Version `v2`

`type` information is a string that is a combination of the following characters:

| Key Character | Information          |
| ------------: | -------------------- |
|           `v` | Vegetarian           |
|           `g` | Vegan                |
|           `p` | Contains Peanuts     |
|           `t` | Contains Tree Nuts   |
|           `w` | Contains Wheat       |
|           `s` | Contains Soy         |
|           `d` | Contains Diary       |
|           `e` | Contains Eggs        |
|           `l` | Contains Shellfish   |
|           `f` | Contains Fish        |
|           `c` | Low-Carbon Footprint |

###### Examples

1. The `type` string `vde` indicates that this entree is vegetarian and contains diary & eggs.
2. The `type` string `tc` indicates that this entree is ordinary, contains tree nuts and is low-carbon footprint.

# License

MIT license, see file `LICENSE`.
