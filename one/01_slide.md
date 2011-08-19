!SLIDE
# Comment j'ai mis du sucre dans mon vin
## François de Metz
## af83

!SLIDE
# Flashback

!SLIDE  bullets incremental
## Il y a deux mois je parlai de

* code javascript expressif
* underscore
* (et je trollais)

!SLIDE bullets
## Une question :
# On ne peut pas étendre le prototype ?

!SLIDE
## Quelques témoignages

!SLIDE
<blockquote>
Le jour ou j'ai étendu le prototype, la suite de test a cassé immédiatement. Depuis j'ai changé et je ne le fait plus.
</blockquote>

<blockquote>
J'ai incorporé une bibliothèque qui avait étendu le prototype de Array. Ma vie a basculé dans l'enfer.
</blockquote>

!SLIDE
# Quels problèmes ?

!SLIDE
## Toute propriété ajoutée devient énumérable.

!SLIDE execute

    @@@ javaScript
    Array.prototype.each = Array.prototype.forEach

    var array = ['Hello', 'World']
    for (var item in array) {
       alert(item)
    }

!SLIDE
## Risque de collision et différence de comportement

!SLIDE
# Quelles avantages ?

!SLIDE
## Sucre Syntaxique++

    @@@javascript
    3.times(function() {})

    "Hello".green

    [1, 2, 3].inject(function(memo, num) {
                         return memo + num;
                     }, 0);

!SLIDE
# Solutions ?

!SLIDE
## Ne pas utiliser for..in
### C'est bien marqué dans la doc ...
### https://developer.mozilla.org/en/JavaScript/Reference/Statements/for...in

!SLIDE
## Étendre le prototype proprement

!SLIDE small execute

    @@@ javaScript
    Object.defineProperty(Array.prototype, 'each', {
        value: function(callback) {
            this.forEach(callback)
        },
        enumerable: false // implicit !
    })

    var array = ['Hello', 'World']
    for (var item in array) {
       alert(item)
    }

!SLIDE small

    @@@javascript
    Object.defineProperty(Array.prototype, 'each', {
        value: ...,
        enumerable: true
    })

!SLIDE center
## Compatibilité :(

Navigateur      | Version
--------------- | -------------
Mozilla Firefox | 4
Google Chrome   | 5
IE              | 9

!SLIDE
## Ne rêgle pas le problème de collision

!SLIDE
# Faites votre choix

!SLIDE
# Questions ?
