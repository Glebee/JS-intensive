## 1)
```
let promiseTwo = new Promise((resolve, reject) => {
  resolve("a");
});

promiseTwo
  .then((res) => {
    return res + "b";
  })
  .then((res) => {
    return res + "с";
  })
  .finally((res) => {
    return res + "!!!!!!!";
  })
  .catch((res) => {
    return res + "d";
  })
  .then((res) => {
    console.log(res); // "abc"
  });
```
## 2)
```
function doSmth() {
  return Promise.resolve("123");
}

doSmth()
  .then(function (a) {
    console.log("1", a); // 1 123
    return a; 
  })
  .then(function (b) {
    console.log("2", b); // 2 123
    return Promise.reject("321");
  })
  .catch(function (err) {
    console.log("3", err); // 3 321
  })
  .then(function (c) {
    console.log("4", c); // 4 undefined
    return c;
  });
```
## 3)
const arr = [10, 12, 15, 21];

let delayedLog = (mass) => {
  for (let i = 0; i < mass.length; i++) {
    setTimeout(() => {
      console.log(mass[i]);
    }, 3000 * (i + 1));
  }
};

delayedLog(arr);

## БОНУС ЗАДАНИЕ
```
async function fetchUrl(url, attemptsAmount = 5) {
  let attempts = 0;

  const fetchAttempt = async () => {
    const response = await fetch(url);

    if (!response.ok) {
      throw new Error(`fail! status: ${response.status}`);
    }

    const data = await response.text();

    console.log("success");

    return data;
  };

  return new Promise((resolve, reject) => {
    const tryFetch = async () => {
      try {
        const result = await fetchAttempt();
        resolve(result);
      } catch (error) {
        console.error(
          `fetching error (attempt ${attempts + 1}/${attemptsAmount}):`,
          error.message
        );

        attempts++;

        if (attempts === attemptsAmount) {
          reject(error);
        } else {
          tryFetch();
        }
      }
    };

    tryFetch();
  });
}

fetchUrl("https://google.com/badURL")
  .then((data) => console.log(data))
  .catch((err) => console.log(err)); // сatch должен сработать только после 5 неудачных попыток
```
