<h1 align="center">My CodinGame Solutions</h1>

- [Classic Puzzle - Easy](#classic-puzzle---easy)
  - [The Descent](#the-descent)
  - [Temperatures](#temperatures)
  - [Defibrillators](#defibrillators)
  - [MIME Type](#mime-type)
  - [Horse-Racing Duals](#horse-racing-duals)

## Classic Puzzle - Easy

### The Descent

[**Puzzle here!**](https://www.codingame.com/training/easy/the-descent)

#### Python

```py
from typing import Tuple

# The while loop represents the game.
# Each iteration represents a turn of the game
# where you are given inputs (the heights of the mountains)
# and where you have to print an output (the index of the mountain to fire on)
# The inputs you are given are automatically updated according to your last actions.


# game loop
while True:
    biggest: Tuple[int, int] = (-1, -1)

    for i in range(8):
        mountain_h = int(input())  # represents the height of one mountain.
        biggest = (i, mountain_h) if biggest[1] < mountain_h else biggest

    # The index of the mountain to fire on.
    print(biggest[0])
```

#### TypeScript

```ts
/**
 * The while loop represents the game.
 * Each iteration represents a turn of the game
 * where you are given inputs (the heights of the mountains)
 * and where you have to print an output (the index of the mountain to fire on)
 * The inputs you are given are automatically updated according to your last actions.
 **/

// game loop
while (true) {
  let biggest: { index: number; height: number };

  for (let i = 0; i < 8; i++) {
    const mountainH: number = parseInt(readline()); // represents the height of one mountain.
    (!biggest || biggest.height < mountainH) &&
      (biggest = { index: i, height: mountainH });
  }

  console.log(biggest.index); // The index of the mountain to fire on.
}
```

#### Java

```java
import java.util.*;

/**
 * The while loop represents the game.
 * Each iteration represents a turn of the game
 * where you are given inputs (the heights of the mountains)
 * and where you have to print an output (the index of the mountain to fire on)
 * The inputs you are given are automatically updated according to your last actions.
 **/
class Player {

    public static void main(String args[]) {
        Scanner in = new Scanner(System.in);

        // game loop
        while (true) {
            Mountain biggest = null;

            for (int i = 0; i < 8; i++) {
                int mountainH = in.nextInt(); // represents the height of one mountain.
                if (biggest == null || biggest.height < mountainH) biggest = new Mountain(i, mountainH);
            }

            System.out.println(biggest.index); // The index of the mountain to fire on.
        }
    }
}

class Mountain {
    public int index;
    public int height;

    public Mountain(int index, int height) {
        this.index = index;
        this.height = height;
    }
}
```

### Temperatures

[**Puzzle here!**](https://www.codingame.com/training/easy/temperatures)

#### TypeScript

```ts
const n: number = parseInt(readline()); // the number of temperatures to analyse
var inputs: string[] = readline().split(' ');

const array: number[] = [];

for (let i = 0; i < n; i++) {
    const t: number = parseInt(inputs[i]);// a temperature expressed as an integer ranging from -273 to 5526
    array.push(t);
}

let closest: {temperature: number; gap: number | null} = {temperature: 0, gap: null};
for (let i = 0; i < array.length; i++) {
    const gap = Math.abs(array[i] - 0);
    const data = {
        temperature: array[i],
        gap
    }
    if (!closest.gap || closest.gap > data.gap || (closest.gap === data.gap && data.temperature > closest.temperature)) closest = data;
}

console.log(closest.temperature);
```

### Defibrillators

[**Puzzle here!**](https://www.codingame.com/training/easy/defibrillators)

#### TypeScript

```ts
const LON: number = parseFloat(readline().replace(",", "."));
const LAT: number = parseFloat(readline().replace(",", "."));
const N: number = parseInt(readline());

let closest = null;

for (let i = 0; i < N; i++) {
  const DEFIB: string = readline();
  const [id, name, adress, phone, lon, lat] = DEFIB.split(";");
  const data = {
    id,
    name,
    adress,
    phone,
    lon: parseFloat(lon.replace(",", ".")),
    lat: parseFloat(lat.replace(",", ".")),
    d: null,
  };
  const x = (data.lon - LON) * Math.cos((LAT + data.lat) / 2);
  const y = data.lat - LAT;
  const d = Math.sqrt(x ** 2 + y ** 2) * 6371;

  data.d = d;

  closest == null || closest.d > data.d
    ? (closest = data)
    : (closest = closest);
}

console.log(closest.name);
```

#### Java

```java
import java.util.*;

class Solution {
    public static Defibrilator closest;

    public static void main(String args[]) {
        Scanner in = new Scanner(System.in);
        String LON = in.next();
        String LAT = in.next();
        int N = in.nextInt();
        if (in.hasNextLine()) {
            in.nextLine();
        }
        for (int i = 0; i < N; i++) {
            String DEFIB = in.nextLine();
            String[] params = DEFIB.split(";");

            Defibrilator defibrilator = new Defibrilator(params[0], params[1], params[2], params[3], params[4], params[5]);

            if (closest == null || closest.getDistance(LON, LAT) > defibrilator.getDistance(LON, LAT)) {
                closest = defibrilator;
            }
        }

        System.out.println(closest.name);
    }
}

class Defibrilator {
    public String id;
    public String name;
    public String adress;
    public String phone;
    public double lon;
    public double lat;

    public Defibrilator(String id, String name, String adress, String phone, String lon, String lat) {
        this.id = id;
        this.name = name;
        this.adress = adress;
        this.phone = phone;
        this.lon = Double.parseDouble(lon.replace(",", "."));
        this.lat = Double.parseDouble(lat.replace(",", "."));
    }

    public double getDistance(String lon, String lat) {
        double lonA = Double.parseDouble(lon.replace(",", "."));
        double latA = Double.parseDouble(lat.replace(",", "."));

        double x = (this.lon - lonA) * Math.cos(Math.toRadians((latA + this.lat) / 2));
        double y = this.lat - latA;

        return Math.sqrt(Math.pow(x, 2) + Math.pow(y, 2)) * 6371;
    }

    @Override
    public String toString() {
        return String.format("id: %s; name: %s; adress: %s; phone: %s; lon: %s; lat: %s", this.id, this.name, this.adress, this.phone, this.lon, this.lat);
    }
}
```

### MIME Type

[**Puzzle here!**](https://www.codingame.com/training/easy/mime-type)

#### TypeScript

```ts
const N: number = parseInt(readline()); // Number of elements which make up the association table.
const Q: number = parseInt(readline()); // Number Q of file names to be analyzed.

const map = new Map();

for (let i = 0; i < N; i++) {
  var inputs: string[] = readline().split(" ");
  const EXT: string = inputs[0]; // file extension
  const MT: string = inputs[1]; // MIME type.
  map.set(EXT.toLowerCase(), MT);
}

for (let i = 0; i < Q; i++) {
  const FNAME: string = readline(); // One file name per line.
  const temp = FNAME.split(".");
  if (temp.length <= 1) {
    console.log("UNKNOWN");
    continue;
  }
  const extension = temp[temp.length - 1].toLowerCase();
  console.error(FNAME, extension);
  map.get(extension) ? console.log(map.get(extension)) : console.log("UNKNOWN");
}
```

### Horse-Racing Duals

[**Puzzle here!**](https://www.codingame.com/training/easy/horse-racing-duals)

#### JavaScript

```js
const N = parseInt(readline());
const temp = [];

for (let i = 0; i < N; i++) {
    temp.push(parseInt(readline()));
}

temp.sort((a, b) => a -b);

let min = Infinity;

for (let i = 1; i < temp.length; i++) {
    min = Math.min(min, temp[i] - temp[i - 1])
}

console.log(min);
```
