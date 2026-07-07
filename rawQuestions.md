# rawQuestions

Extracted from `index.html`.

## Question 1

```js
new Date("0")
```

### Options

- 1970-01-01T00:00:00.000Z
✅ 2000-01-01T00:00:00.000Z
- Invalid Date
- Throws an error

### Explanation

The string "0" is interpreted as the year 2000, not as a timestamp!

## Question 2

```js
new Date(0)
```

### Options

✅ 1970-01-01T00:00:00.000Z
- 2000-01-01T00:00:00.000Z
- Invalid Date
- Throws an error

### Explanation

The *number* 0, as opposed to the string "0", is interpreted as milliseconds since the Unix epoch (Jan 1, 1970).

## Question 3

```js
Date.parse(0) === Date.parse("0")
```

### Options

✅ true
- false
- Throws an error
- undefined

### Explanation

Both parse to 946684800000 milliseconds! Date.parse only operates on strings, so 0 is coerced to the string "0".

## Question 4

```js
new Date("not a date")
```

### Options

- null
- undefined
✅ Invalid Date
- Throws an error

### Explanation

Invalid Date is still a Date object! It's not null or an error.

## Question 5

```js
new Date("not a date").getTime()
```

### Options

- 0
✅ NaN
- null
- Throws an error

### Explanation

Invalid Date objects return NaN for getTime(). This function returns the number of milliseconds since the Unix epoch for valid dates.

## Question 6

```js
new Date("not a date").toISOString()
```

### Options

- "Invalid Date"
- null
- NaN
✅ Throws an error

### Explanation

toISOString() throws a RangeError on Invalid Date objects.

## Question 7

```js
new Date("not a date").toTimeString()
```

### Options

✅ "Invalid Date"
- ""
- null
- Throws an error

### Explanation

toTimeString() returns the string "Invalid Date" for invalid dates. 🫠

## Question 8

```js
new Date("1")
```

### Options

- 1970-01-01T00:00:01.000Z
✅ 2001-01-01T00:00:00.000Z
- 0001-01-01T00:00:00.000Z
- Invalid Date

### Explanation

Unlike "0", "1" is interpreted as a month, and the year defaults to 2001 for some reason.

## Question 9

```js
new Date("2")
```

### Options

- 2002-01-01T00:00:00.000Z
- 2001-01-02T00:00:00.000Z
✅ 2001-02-01T00:00:00.000Z
- Invalid Date

### Explanation

"2" is interpreted as February 2001 (month 2), as you might expect from the previous question.

## Question 10

```js
new Date("12")
```

### Options

- 2012-01-01T00:00:00.000Z
- 2001-01-12T00:00:00.000Z
✅ 2001-12-01T00:00:00.000Z
- Invalid Date

### Explanation

Also works for December.

## Question 11

```js
new Date("13")
```

### Options

- 2013-01-01T00:00:00.000Z
- 2001-01-13T00:00:00.000Z
- 2001-13-01T00:00:00.000Z
✅ Invalid Date

### Explanation

"13" would be month 13, which doesn't exist, so it's Invalid Date.

## Question 12

```js
new Date("99") > new Date("100")
```

### Options

✅ true
- false
- Throws an error
- NaN

### Explanation

"99" is year 1999, while "100" is year 0100. 1999 > 0100! Date starts interpreting numbers as years starting at "32".

## Question 13

```js
new Date("49") > new Date("50")
```

### Options

✅ true
- false
- Throws an error
- NaN

### Explanation

And for some reason "32" to "49" is 2032-2049, while "50" onwards is 1950+. So 2049 > 1950!

## Question 14

```js
new Date("12.1")
```

### Options

✅ 2001-12-01T00:00:00.000Z
- 2001-01-01T00:00:00.000Z
- 2012-01-01T00:00:00.000Z
- Invalid Date

### Explanation

"12.1" is interpreted as the date December 1st, and as before for dates with no year the default is 2001 because of course.

## Question 15

```js
new Date("12.0")
```

### Options

- 2012-01-01T00:00:00.000Z
- 2001-12-01T00:00:00.000Z
- 2001-01-12T00:00:00.000Z
✅ Invalid Date

### Explanation

The .0 is still interpreted as a day, and no month has a 0th day, so this is considered invalid.

## Question 16

```js
new Date("12.-1")
```

### Options

✅ 2001-12-01T00:00:00.000Z
- 2001-01-01T00:00:00.000Z
- 2012-01-01T00:00:00.000Z
- Invalid Date

### Explanation

The dash here is ignored, so this is interpreted the same as "12.1".

## Question 17

```js
new Date("perhaps 1")
```

### Options

- Invalid Date
✅ 2001-01-01T00:00:00.000Z
- 1970-01-01T00:00:01.000Z
- Throws an error

### Explanation

Leading text is always ignored! It finds the "1" and parses it as the month January.

## Question 18

```js
new Date("perhaps")
```

### Options

✅ Invalid Date
- 2001-01-01T00:00:00.000Z
- 1970-01-01T00:00:01.000Z
- Throws an error

### Explanation

But you can't *just* have text! It needs a number to parse, so this is Invalid Date. It's equivalent to new Date("").

## Question 19

```js
new Date("maybe 1")
```

### Options

- 2001-01-01T00:00:00.000Z
✅ 2001-04-30T23:00:00.000Z
- 2001-05-01T00:00:00.000Z
- Invalid Date

### Explanation

"may" in "maybe" is parsed as the month May! The exact output depends on the local timezone used when the date is evaluated.

## Question 20

```js
new Date("fourth of may 2010")
```

### Options

- Invalid Date
- 2010-05-04T00:00:00.000Z
✅ 2010-04-30T23:00:00.000Z
- 2010-05-01T00:00:00.000Z

### Explanation

"fourth of" is ignored, this is just parsing "may 2010", and the exact output depends on the local timezone used when the date is evaluated.

## Question 21

```js
new Date("May 4 UTC")
```

### Options

- Invalid Date
✅ 2001-05-04T00:00:00.000Z
- 2010-04-30T23:00:00.000Z
- 2010-05-01T00:00:00.000Z

### Explanation

UTC is correctly parsed as a timezone.

## Question 22

```js
new Date("May 4 UTC+1")
```

### Options

- Invalid Date
- 2001-05-04T00:00:00.000Z
✅ 2001-05-03T23:00:00.000Z
- 2010-05-01T00:00:00.000Z

### Explanation

You can add modifiers to timezones and it works as you would expect.

## Question 23

```js
new Date("May 4 UTC+1:59")
```

### Options

- Invalid Date
- 2001-05-04T00:00:00.000Z
✅ 2001-05-03T22:01:00.000Z
- Throws an error

### Explanation

It also supports minutes!

## Question 24

```js
new Date("May 4 UTC+1:60")
```

### Options

- Invalid Date
- 2001-05-04T00:00:00.000Z
- 2001-05-03T22:00:00.000Z
✅ 1960-05-03T23:00:00.000Z

### Explanation

Until it doesn't! 60 is being parsed as the year here, UTC+1 is the timezone.

## Question 25

```js
new Date("1990 2010")
```

### Options

- 1990-01-01T00:00:00.000Z
- 2010-01-01T00:00:00.000Z
- 2000-01-01T00:00:00.000Z
✅ Invalid Date

### Explanation

No tricks here, just a plain ol' Invalid Date.

## Question 26

```js
new Date("1990 (2010)")
```

### Options

✅ 1990-01-01T00:00:00.000Z
- 2010-01-01T00:00:00.000Z
- 2000-01-01T00:00:00.000Z
- Invalid Date

### Explanation

For some reason, parenthesised text is ignored.

## Question 27

```js
new Date("(1990) 2010")
```

### Options

- 1990-01-01T00:00:00.000Z
✅ 2010-01-01T00:00:00.000Z
- 2000-01-01T00:00:00.000Z
- Invalid Date

### Explanation

No matter where it is.

## Question 28

```js
new Date(-[])
```

### Options

✅ 1970-01-01T00:00:00.000Z
- 2000-01-01T00:00:00.000Z
- Throws an error
- Invalid Date

### Explanation

I couldn't resist. -[] is coerced to 0, which is interpreted as milliseconds since the Unix epoch (Jan 1, 1970).
