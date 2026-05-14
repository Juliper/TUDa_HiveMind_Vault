---
title: FMISE
aliases:
  - Formale Methoden im Softwareentwurf
tags:
  - fb20
  - bachelor
  - semester-4
  - 5CP
description: ""
draft: false
---
# Promela (SPIN)

### Datentypen

- byte, short, int, unsigned
- bit b1 = 1 same bool b2 = true
- mtype = { red , yellow , green }; (message types)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fe0d6b9e-cd89-46db-bfbc-0f6d994cd5d5/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6a84c866-4b93-48e3-a07d-2b16471d389f/Untitled.png)

### Selection

Wählt zufällig einen wahren block. Falls keiner wahr wird blockiert bis einer wahr ist.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a52bbf42-b80a-4f71-9a0b-d582eadf4daf/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7499cbf3-d4d9-4b84-9f63-0337fcd65de2/Untitled.png)

### Repetition

Wählt zufällig einen wahren block. Falls keiner wahr wird blockiert bis einer wahr ist.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4e842e62-df44-4f97-8a58-c212852429cc/Untitled.png)

### For-Loop

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9f3cf526-80ed-45c7-a300-5cc7f17a9ec6/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8d816f7c-c751-4755-99bd-a601b4b817ca/Untitled.png)

### Jumps

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/50436f7e-fe69-47fe-9d82-9918a0f1fce4/Untitled.png)

### Inline

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2d2688bc-131e-4184-9836-91544411a1d3/Untitled.png)

### Zufällige Werte

true → kann weggelassen werden

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7b38671b-5bfd-4f42-94ed-e1e9de9ac346/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/928e98a0-2e0b-4991-b7bd-3b74d0c80d77/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c75ac83e-6389-4a76-b98c-a9aa9d607231/Untitled.png)

### Mehrere Prozesse

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2aa7f0f4-0339-4041-a702-2485c746a18e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b4fd93b0-5b0a-43ac-b067-a42cda89024f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f22655bf-8f91-4b44-9ad0-55b355401d5e/Untitled.png)

### Atomic

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e57e0397-9b9d-448a-8200-208cce039a18/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8a717089-942a-402f-97cb-dc1a26153b94/Untitled.png)

### Initial Prozess

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/87fdb93e-54b9-4fde-b0cd-b9d260d54142/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ce38b77f-5c73-4dd7-8525-404dc88c939f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ee9b7856-1bb3-435b-97b4-88257e10248e/Untitled.png)

### Assert

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/178152b4-c799-423d-81f1-4e0b09582b25/Untitled.png)

### Endstate

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/60f71da1-82d4-4b98-b80e-e248438bb2f0/Untitled.png)

### Channels

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3cb14a07-dd11-4793-be6b-ce84841ae533/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ec4df8a5-8f08-4eff-b93f-998d0e03806f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/874f3b81-35c9-484d-bdd0-ff3fc5b34c2e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/78d00c5e-1538-4857-81d9-d19bb281280f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a394063b-d263-4da4-aa08-e321e1f218f0/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/820fe939-6f42-4ca8-85f7-686b3a2445ac/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/190b4fc8-6ac2-4ac7-9524-f32a31e5766e/Untitled.png)

# Propositional Logic

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7793d81a-a7af-4441-a050-4dc65480b6f6/Untitled.png)

# Temporal Logic

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e708a98d-4a96-4139-a49d-2c3f05d460d8/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b3e427ea-c29e-40f0-9f1c-4a34d71fb0ac/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1aef9173-d8da-4cdf-863e-3622c6c3a8f6/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/52716fb7-d52c-4bb1-aeeb-5b7f73e2e47b/Untitled.png)

# Büchi Automat

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/18dbf4e7-830d-4f57-9479-38bea8b68944/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4b4dc50a-c45b-40ae-8713-dc67a918129a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/83b49f76-fa58-43fc-9618-22aac5827158/Untitled.png)

# Automat in Promela

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/26c0a975-c7f8-4e8e-9935-c9b9e00c5962/Untitled.png)

```c
mtype = {login, logout} 

inline selectEvent(event) {
  if
   :: event = login
   :: event = logout
  fi   
}

active proctype Authentication() {
   byte fail = 0;
   byte currentState = 0;
   mtype ev;

   do
      :: currentState == 0 ->
         printf("Init");
         selectEvent(ev);
         if
            :: fail >= 3 -> currentState = 2
            :: fail < 3  && ev == login  ->  fail = 0; currentState = 1
            :: fail < 3  && ev == login  ->  fail = fail + 1; currentState = 0
			   fi
      :: currentState == 1 -> 
         printf("Authenticated"); 
         selectEvent(ev); 
         if
            :: ev == logout -> currentState = 0
			   fi 
      :: currentState == 2 -> printf("Locked"); selectEvent(ev)        
   od
}
```

# FOL

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6f1299c6-608a-4810-85a3-ead239391356/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d6d1fd5f-fd70-4597-bebc-f0fbf5b1fa3d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9cda15d6-bfa4-45f6-8230-0064d4005dfc/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/948640e1-3892-4f75-8567-a03e715c3dd9/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/55e49c63-808c-4bd6-86de-d4a9e6e7c70c/Untitled.png)

# JML

# DL

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/83fadb4c-5518-4ffc-a000-9e171c1014ff/Untitled.png)

# Altklausuren Aufgaben

## LTL Formel, Büchiautomaten und ω-reguläre Ausdrücke

### LTL Formeln

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/311ec45c-eb6a-40ce-afed-d81f3a9e558f/Untitled.png)

[]<> := Es wird unendlich oft wahr

<>[] := irgendwann ist es unendlich lange wahr

not[]A == <>not A und not <> A == [] not A

Interpreationen so angeben := $I = \{p, q\}$ bedeutet Interpretation in der p und q wahr sind

LTL in promela

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/15243586-99d6-41db-ab33-d4785f0cd800/Untitled.png)

### Büchiautomaten

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9e44a705-0a3b-4833-a957-b0b1dd2cec16/Untitled.png)

### ω-reguläre Ausdrücke

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7733ff3b-a40c-430a-a590-6f983f99836d/Untitled.png)

## Sequenzenkalkül

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3288ae0c-d76d-4432-912d-8532b9698cbb/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/715104fa-2b57-4fe0-a3c9-9ed564a35dca/Untitled.png)

Bei allRight und exLeft muss c ein komplett neues Symbol sein

Bei Quantoren gilt

$\phi \Rightarrow \lnot\exists x;\psi$ wird zu $\phi,\exists x;\psi \Rightarrow$ (auch bei forall)

## JML

### Public invariant

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f5d4f298-2aa9-4091-a605-5d1295c88822/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4e640b24-f157-4ec0-a404-d15b90cd5d97/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/12d322d9-01d0-4d8e-a9f1-2b43eb7fdfbc/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5da8fb65-1d17-4ea0-ad4c-fa5d27912c53/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/739358b8-3426-418b-8ecc-b0526fdbbbec/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3fd50c29-63ba-4b8e-8cb1-fd1a6c353dcf/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9373b72e-81d7-4f6f-a436-9732c62d7208/Untitled.png)

### Methoden Spezifikation

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5a8b98ed-7475-4426-8dad-c46977474c40/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/143e476d-45d8-4d03-8ca9-83c1f0aec88d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a16f26ff-1d51-46bd-83a2-3d890ba0c42e/Untitled.png)

### Schleifeninvariante

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3de2b453-d48b-40a1-84e5-e2b938288b69/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/29e0e7a9-d9b6-4112-bd50-b3d2f4ac123d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/31e3369d-157b-487a-9c26-7fef4900d198/Untitled.png)

## Promela

- _nr_pr built-in variable holding number of running processes
- _pid Prozess ID
- select ( i : 0 .. 4);
- assert ()
- active [2] proctype Authentication() {}
- chan myChan = [0] of { byte }
- atomic { condition −> statement1; ... statementK; } führt alle statements atomar aus, wenn die Bedingung wahr ist (und keines der Statements blockt). Ansonsten blockiert der Prozess solange bis die Bedingung wahr wird. (Details und ganze Wahrheit in der nächsten Vorlesung)
- for (i: 0..9) {}

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/615ee66c-2904-4935-ba4c-f38db1160f85/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/df3c10ed-4158-4a87-b6db-32a304b41829/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b233e814-95bf-4334-bcf2-760645bfddfe/Untitled.png)

## FOL

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6f1299c6-608a-4810-85a3-ead239391356/Untitled.png)

Formel auswertung

- $val_{S, \beta}(p(t_1,...,t_n)) = T ~~iff~~(val_{S,\beta}(t_1),...,val_{S,\beta}(t_n)) \in I(p)$ (Prädikate)
- $val_{S, \beta}(f(x)) = T ~~iff~~I(f)val_{S, \beta}(x)$
- $val_{S, \beta}(x) = T ~~iff~~ I(x)~~oder~~ \beta(x)$
- Übung 7 nochmal angucken

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d6d1fd5f-fd70-4597-bebc-f0fbf5b1fa3d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9cda15d6-bfa4-45f6-8230-0064d4005dfc/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/55e49c63-808c-4bd6-86de-d4a9e6e7c70c/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c346b44e-f38b-4345-a299-a10074b3fee0/Untitled.png)

## DL

### DL Bedeutung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e58aaa8d-dccd-43b7-9b44-681a6f2bbf9e/Untitled.png)

Falls i > 0 gilt, dann terminiert die Zuweisung und der neue Wert von i größer oder gleich 0.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0ab00914-27bf-405e-a099-5a59fa1b20c3/Untitled.png)

Falls i > 0 gilt und die Schleife terminiert, dann ist der Wert von i 1.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0bfd6c24-5ce4-41c9-bd1a-eef52edd22d0/Untitled.png)

Es gibt ein Booleanwert, so dass nachdem b diesen Wert zugewiesen bekommen hat, das Programm terminiert und für die neuen Werte i= 0 gilt.

### JML zu DL

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f3ef6fd9-d845-4060-a081-169f15e8a86d/Untitled.png)

## State Updates

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/56bbf7b1-ca13-411b-8a8f-e47dfd145a05/Untitled.png)

Regeln

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/40e56539-d8ab-4643-9ff2-f09551d3fe1f/Untitled.png)
