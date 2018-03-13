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
    $('#demo-img').attr("src", "");

    var a = Rx.Observable.create(function (handle) {
        console.log('%ccreated outer observable', 'color:red;');

        setTimeout(function () {
            handle.next('10ms-outer');
        }, 10);

        setTimeout(function () {
            handle.next('550ms-outer')
        }, 600);

        setTimeout(function () {
            handle.next('950ms-outer');
            handle.complete();
        }, 900);

        return function() {
            console.log('%couter observable complete', 'color:red;');
        };

    });

    var b = Rx.Observable.create(function (handle) {
        console.log('%c  inner started', 'color:green;');

        setTimeout(function () {
            handle.next('  500ms-inner');
        }, 500);

        setTimeout(function () {
            handle.next('  1000ms-inner')
        }, 1000);

        setTimeout(function () {
            handle.next('  1500ms-inner');
            handle.complete();
        }, 1500);

        return function() {
            console.log('%c  inner complete', 'color:green;');
        };

    });


    a.do(function (val) {
        console.log(val);
    }).map(function () {
        return b;
    }).switch()
        .subscribe({
            next: function (val) {
                console.log(val);
            }
        });

});
```
