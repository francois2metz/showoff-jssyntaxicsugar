!SLIDE
# Comment j'ai mis du sucre dans mon vin
## François de Metz
## af83

!SLIDE
# Comment rajouter du sucre syntaxique en modifiant le prototype

!SLIDE
# Flashback

!SLIDE  bullets incremental
## Il y a deux mois je vous parlais de

* code javascript expressif
* underscore
* (et je trollais)

!SLIDE bullets
# Une question: On peut pas étendre le prototype ?

!SLIDE
# Quelles problèmes ?

!SLIDE
## Toute propriété ajouté devient énumérable.

!SLIDE execute

    @@@ javaScript
    Array.prototype.each = function(callback) {
        this.forEach(callback)
    }

    var array = ['Hello', 'World']
    for (var item in array) {
       alert(item)
    }

!SLIDE
## Risque de collision et différence de comportement

!SLIDE
### Quelques témoignages

<blockquote>
Le jour ou j'ai étendu le prototype, la suite de test a cassé immédiatement. Depuis j'ai changé et je ne le fait plus.
</blockquote>

!SLIDE

<blockquote>
J'ai incorporé une bibliothèque qui avait étendu le prototype de Array. Ma vie a basculé dans l'enfer.
</blockquote>

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

!SLIDE small
# Getter/setter

    @@@javascript
    Object.defineProperty(Array.prototype, 'myLength', {
        get: function() {
        
        },
        set: function(value) {
        
        }
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
