# Pourquoi il ne faut pas utiliser `using namespace std` en C++ ?  

## Mais ça me fait gagner du temps ! 

Tu gagnes vraiment du temps à ne pas écrire 5 caractères ? Même moi avec le placement catastrophique de mes doigts sur mon clavier je perd même pas une seconde à l'écrire. Et le temps que tu mettras à régler tes problèmes quand tu en aura à cause du `using namespace std`  sera bien supérieur à celui que tu auras économisé en ne tapant pas 5 caractères.

## Pourquoi ça existe s'il faut pas l'utiliser ?

Cette ligne est là car à une époque, le C++ ne possédait pas le concept de namespace, donc toute les fonctions, classes, etc... de la bibliothèque standard n'avaient pas de namespace, mais à l'arrivée du C++ moderne qui embarquait les namespaces, toute la bibliothèque standard à été décalée dans le namespace std, et pour ne pas compliquer la vie des développeurs qui avaient déjà des programmes en C++ à l'époque, ils ont décidé d'ajouter le `using namespace std`.

## Pourquoi je ne dois pas l'utiliser

Imagine que tu as un namespace `foo` et un namespace `bar` qui se présentent sous cette forme :

```cpp
#include <iostream>

namespace foo {
  void foo() {
     std::cout << "foo" << std::endl;
  }
}

namespace bar {
  void bar() {
    std::cout << "bar" << std::endl;
  }
}

using namespace foo;
using namespace bar;

int main() {
  foo(); // affiche foo
  bar(); // affiche bar
}
```
là ça ne pose aucun problème mais imagine qu'ensuite tu ajoutes une fonction foo dans le namespace `bar`

```cpp
#include <iostream>

namespace foo {
  void foo() {
     std::cout << "foo" << std::endl;
  }
}

namespace bar {
  void foo() {
    std::cout << "foo mais dans bar" << std::endl;
  }

  void bar() {
    std::cout << "bar" << std::endl;
  }
}

using namespace foo;
using namespace bar;

int main() {
  foo(); // ???
  foo(); // ???
  bar(); // affiche bar
}
```

le compilateur saura pas quoi faire mais si tu avais directement fait  

```cpp
#include <iostream>

namespace foo {
  void foo() {
     std::cout << "foo" << std::endl;
  }
}

namespace bar {
  void foo() {
    std::cout << "foo mais dans bar" << std::endl;
  }

  void bar() {
    std::cout << "bar" << std::endl;
  }
}

int main() {
  foo::foo(); // affiche "foo"
  bar::foo(); // affiche "foo mais dans bar"
  bar::bar(); // affiche bar
}
```

tu aurais eu aucun problème et t'aurais pas passé du temps à régler le problème.

### English version  

If you want to see the English translation click [here](README-en.md)  
*The translation may not be 100% accurate. If you want to correct any error you can submit a pull request.*  