# Creating 

## Observables

```JavaScript
var observable = Rx.Observable.create(function subscribe(observer) {
  var id = setInterval(() => {
    observer.next('hi')
  }, 1000);
});
```

## Observers

```
var observer = {
  next: x => console.log('Observer got a next value: ' + x),
  error: err => console.error('Observer got an error: ' + err),
  complete: () => console.log('Observer got a complete notification'),
};
```

## Subscriptions

```
var observable = Rx.Observable.interval(1000);
var subscription = observable.subscribe(x => console.log(x));
// Later:
// This cancels the ongoing Observable execution which
// was started by calling subscribe with an Observer.
subscription.unsubscribe();
```

## Subjects
```
var subject = new Rx.Subject();

subject.subscribe({
  next: (v) => console.log('observerA: ' + v)
});
subject.subscribe({
  next: (v) => console.log('observerB: ' + v)
});

subject.next(1);
subject.next(2);
```

## Behavior Subjects
```
var subject = new Rx.BehaviorSubject(0); // 0 is the initial value

subject.subscribe({
  next: (v) => console.log('observerA: ' + v)
});

subject.next(1);
subject.next(2);

subject.subscribe({
  next: (v) => console.log('observerB: ' + v)
});

subject.next(3);
```

# Combining Observables

## Merge

```
$('document').ready(function () {
    $('#title').text('MERGE');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*VAHTR8hAmOpum8IFrdzZlA.gif");
});

const a = Rx.Observable.interval(100).take(3)
    .map((i) => ['0-a','1-a','2-a'][i]);

const b = Rx.Observable.interval(150).take(3)
    .map((i) => ['0-b','1-b','2-b'][i]);

Rx.Observable.merge(a,b)
    .subscribe(val => console.log(val));
```

## Concat

```
$('document').ready(function () {
    $('#title').text('CONCAT');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*I_fiTaQJG0Lm8SOyttFxHQ.gif");;
});

const a = Rx.Observable.interval(100).take(3)
    .map((i) => ['0-a','1-a','2-a'][i]);

const b = Rx.Observable.interval(200).take(3)
    .map((i) => ['0-b','1-b','2-b'][i]);

Rx.Observable.concat(a,b)
    .subscribe(val => console.log(val));
```

## Race

```
$('document').ready(function () {
    $('#title').text('RACE');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*rMlMQMO2oRecJ408HH4ngQ.gif");
});

const a = Rx.Observable.interval(100).take(3)
    .map((i) => ['0-a','1-a','2-a'][i]);

const b = Rx.Observable.interval(200).take(3)
    .map((i) => ['0-b','1-b','2-b'][i]);

Rx.Observable.race(a,b)
    .subscribe(val => console.log(val));
```

# Higher Level Observables - combining, projection with flattening

## mergeAll and mergeMap

```
$('document').ready(function () {
    $('#title').text('MERGE ALL');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*yD7NacIon9ohZT_pKS_04w.gif");
});

const a = Rx.Observable.interval(140).take(3)
    .map((i) => ['0-a','1-a','2-a'][i]);

const b = Rx.Observable.interval(150).take(3)
    .map((i) => ['0-b','1-b','2-b'][i]);

const h = Rx.Observable.interval(20).take(2)
    .map((i) => [a,b][i]);

h.mergeAll().subscribe(val => console.log(val));
```

## concatAll and concatMap

```
$('document').ready(function () {
    $('#title').text('CONCAT ALL');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*d1eoR9PyxBPg9btT4o6pGA.gif");
});

const a = Rx.Observable.interval(100).take(3)
    .map((i) => ['0-a','1-a','2-a'][i]);

const b = Rx.Observable.interval(150).take(3)
    .map((i) => ['0-b','1-b','2-b'][i]);

const h = Rx.Observable.interval(50).take(2)
    .map((i) => [a,b][i]);

h.concatAll().subscribe(val => console.log(val));
```

## switch and switchMap

```
$('document').ready(function () {
    $('#title').text('SWITCH');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*OZQs3nPxTxE3IZ-pTnDxLQ.gif");

    // http://reactivex.io/documentation/operators/images/switch.c.png
});

const a = Rx.Observable.interval(100).take(3)
    .map((i) => ['0-a','1-a','2-a'][i]);

const b = Rx.Observable.interval(200).take(3)
    .map((i) => ['0-b','1-b','2-b'][i]);

const h = Rx.Observable.interval(100).take(2)
    .map((i) => [a,b][i]);

h.switch().subscribe(val => console.log(val));

```

# Operators

## combineLatest

```
$('document').ready(function () {
    $('#title').text('COMBINE LATEST');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*uh5Db_W2CixKpK9LlYkURQ.gif");
});

const a = Rx.Observable.interval(100).take(3)
    .map((i) => ['0-a','1-a','2-a'][i]);

const b = Rx.Observable.interval(150).take(3)
    .map((i) => ['0-b','1-b','2-b'][i]);

Rx.Observable.combineLatest(a,b).subscribe(val => console.log(val));
```

## zip

```
$('document').ready(function () {
    $('#title').text('ZIP');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*Cu-uSXNacbLlpWjm35C3_Q.gif");
});

const a = Rx.Observable.interval(100).take(3)
    .map((i) => ['0-a','1-a','2-a'][i]);

const b = Rx.Observable.interval(150).take(3)
    .map((i) => ['0-b','1-b','2-b'][i]);

Rx.Observable.zip(a,b).subscribe(val => console.log(val));
```

## forkJoin

```
$('document').ready(function () {
    $('#title').text('FORK JOIN');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*dsH5d-_64TXBFlEr7YCAqQ.gif");
});

const a = Rx.Observable.interval(100).take(3)
    .map((i) => ['0-a','1-a','2-a'][i]);

const b = Rx.Observable.interval(150).take(3)
    .map((i) => ['0-b','1-b','2-b'][i]);

Rx.Observable.forkJoin(a,b).subscribe(val => console.log(val));
```

## withLatestFrom

```
$('document').ready(function () {
    $('#title').text('WITH LATEST FROM');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*ZhM7RAp_LctDt7kuOuisGA.gif");
});

const a = Rx.Observable
    .interval(100).take(3)
    .map((i) => ['0-a','1-a','2-a'][i]);

const b = Rx.Observable
    .interval(150).take(3)
    .map((i) => ['0-b','1-b','2-b'][i]);

b.withLatestFrom(a).subscribe(val => console.log(val));
```
