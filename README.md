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
    $('#title').text('MERGE');
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
