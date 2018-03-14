# rxjs-presentation

# 01 Merge

```
$('document').ready(function () {
    $('#title').text('MERGE');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*VAHTR8hAmOpum8IFrdzZlA.gif");

    var a = Rx.Observable.create(function(handle) {
        handle.next('0-a');

        setTimeout(function() {
            handle.next('1-a')
        }, 200);

        setTimeout(function() {
            handle.next('2-a');
            handle.complete();
        }, 300);

    });

    var b = Rx.Observable.create(function(handle) {
        handle.next('0-b');

        setTimeout(function() {
            handle.next('1-b')
        }, 200);

        setTimeout(function() {
            handle.next('2-b');
            handle.complete();
        }, 350);

    });

    Rx.Observable.merge(a,b)
        .subscribe({
            next: function(val) {
                console.log(val);
            }
        });

});
```

# 02 Concat

```
$('document').ready(function () {
    $('#title').text('CONCAT');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*I_fiTaQJG0Lm8SOyttFxHQ.gif");

    var a = Rx.Observable.create(function(handle) {
        handle.next('0-a');
        
        setTimeout(function() {
            handle.next('1-a')
        }, 200);
        
        setTimeout(function() {
            handle.next('2-a');
            handle.complete();
        }, 300);

    });

    var b = Rx.Observable.create(function(handle) {
        handle.next('0-b');
        
        setTimeout(function() {
            handle.next('1-b')
        }, 200);
        
        setTimeout(function() {
            handle.next('2-b');
            handle.complete();
        }, 250);

    });

    Rx.Observable.concat(a,b)
        .subscribe(function(val) {
            console.log(val);
        });

});
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

# 03 Race

```
$('document').ready(function () {
    $('#title').text('RACE');
    $('#demo-img').attr("src", "https://cdn-images-1.medium.com/max/800/1*rMlMQMO2oRecJ408HH4ngQ.gif");

    var a = Rx.Observable.create(function(handle) {
        handle.next('0-a');
        
        setTimeout(function() {
            handle.next('1-a')
        }, 200);
        
        setTimeout(function() {
            handle.next('2-a');
            handle.complete();
        }, 300);

    });

    var b = Rx.Observable.create(function(handle) {
        handle.next('0-b');
        
        setTimeout(function() {
            handle.next('1-b')
        }, 200);
        
        setTimeout(function() {
            handle.next('2-b');
            handle.complete();
        }, 250);

    });

    Rx.Observable.race(a,b)
        .subscribe(function(val) {
            console.log(val);
        });

});
```

# 04 Switch

```
$('document').ready(function () {
    $('#title').text('SWITCH');
    $('#demo-img').attr("src", "http://reactivex.io/documentation/operators/images/switch.c.png");

    const outerObservable = Rx.Observable.create((observer) => {
        console.log('%ccreated outer observable', 'color:red;');

        setTimeout(() => {
            observer.next('10ms-outer');
        }, 10);

        setTimeout(() => {
            observer.next('550ms-outer')
        }, 600);

        setTimeout(() => {
            observer.next('950ms-outer');
            observer.complete();
        }, 900);

        return () => {
            console.log('%couter observable complete', 'color:red;');
        };

    });

    const innerObservable = Rx.Observable.create((observer) => {
        console.log('%c  inner started', 'color:green;');

        setTimeout(() => {
            observer.next('  500ms-inner');
        }, 500);

        setTimeout(() => {
            observer.next('  1000ms-inner')
        }, 1000);

        setTimeout(() => {
            observer.next('  1500ms-inner');
            observer.complete();
        }, 1500);

        return () => {
            console.log('%c  inner complete', 'color:green;');
        };

    });


    outerObservable.do(val => {
        console.log(val);
    }).map(() => innerObservable)
        .switch()
        .subscribe({
            next: function (val) {
                console.log(val);
            }
        });
});
```
