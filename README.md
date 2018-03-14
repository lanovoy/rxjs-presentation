# rxjs-presentation

# 01 Merge

```
$('document').ready(function () {
    $('#title').text('MERGE');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*VAHTR8hAmOpum8IFrdzZlA.gif");
});

const a = Rx.Observable.interval(100).take(3).map((i) => ['0-a','1-a','2-a'][i]);
const b = Rx.Observable.interval(150).take(3).map((i) => ['0-b','1-b','2-b'][i]);

Rx.Observable.merge(a,b)
    .subscribe(val => console.log(val));
```

# 02 Concat

```
$('document').ready(function () {
    $('#title').text('CONCAT');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*I_fiTaQJG0Lm8SOyttFxHQ.gif");;
});

const a = Rx.Observable.interval(100).take(3).map((i) => ['0-a','1-a','2-a'][i]);
const b = Rx.Observable.interval(200).take(3).map((i) => ['0-b','1-b','2-b'][i]);

Rx.Observable.concat(a,b)
    .subscribe(val => console.log(val));
```

## Merge and Concat additional sample

```
// Simulate HTTP requests
const getPostOne$ = Rx.Observable.timer(3000)
    .mapTo('1st finished').startWith('1st started');
const getPostTwo$ = Rx.Observable.timer(1000)
    .mapTo('2nd finished').startWith('2nd started');

Rx.Observable.merge(getPostOne$, getPostTwo$)
    .subscribe(res => console.log(res));
```

# Race

```
$('document').ready(function () {
    $('#title').text('RACE');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*rMlMQMO2oRecJ408HH4ngQ.gif");
});

const a = Rx.Observable.interval(100).take(3).map((i) => ['0-a','1-a','2-a'][i]);
const b = Rx.Observable.interval(200).take(3).map((i) => ['0-b','1-b','2-b'][i]);

Rx.Observable.race(a,b)
    .subscribe(val => console.log(val));
```

# mergeAll and mergeMap

```
$('document').ready(function () {
    $('#title').text('MERGE ALL');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*yD7NacIon9ohZT_pKS_04w.gif");
});

const a = Rx.Observable.interval(140).take(3).map((i) => ['0-a','1-a','2-a'][i]);
const b = Rx.Observable.interval(150).take(3).map((i) => ['0-b','1-b','2-b'][i]);
const h = Rx.Observable.interval(20).take(2).map((i) => [a,b][i]);

h.mergeAll().subscribe(val => console.log(val));
```

# concatAll and concatMap

```
$('document').ready(function () {
    $('#title').text('CONCAT ALL');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*d1eoR9PyxBPg9btT4o6pGA.gif");
});

const a = Rx.Observable.interval(100).take(3).map((i) => ['0-a','1-a','2-a'][i]);
const b = Rx.Observable.interval(150).take(3).map((i) => ['0-b','1-b','2-b'][i]);
const h = Rx.Observable.interval(50).take(2).map((i) => [a,b][i]);

h.concatAll().subscribe(val => console.log(val));
```

# switch and switchMap

```
$('document').ready(function () {
    $('#title').text('SWITCH');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*OZQs3nPxTxE3IZ-pTnDxLQ.gif");

    // http://reactivex.io/documentation/operators/images/switch.c.png
});    

const a = Rx.Observable.interval(100).take(3).map((i) => ['0-a','1-a','2-a'][i]);
const b = Rx.Observable.interval(200).take(3).map((i) => ['0-b','1-b','2-b'][i]);
const h = Rx.Observable.interval(100).take(2).map((i) => [a,b][i]);

h.switch().subscribe(val => console.log(val));

```

