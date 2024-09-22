# markdown mermaid

> 网站<https://mermaid.nodejs.cn/intro/>

## sequenceDiagram

```mermaid
sequenceDiagram;
participant A as Agency
participant B as Purchaser
participant C as monitor

autoNumber

A->>B: 实线箭头;
activate B;
B-->>C: 虚线箭头
A->+B: 实线无箭头
B-->C: 虚线无箭头
A-XB: 实线带x
B--XC: 虚线带x
A-)B: 实线带尖角
B--)C: 虚线带尖角

```

[more](https://blog.csdn.net/Tuing_/article/details/129875279)

## flowchart

```mermaid
flowchart LR
    markdown["`This **is** _Markdown_`"]
    newLines["`Line1
    Line 2
    Line 3`"]
    markdown --> newLines

    roundedRectangle(圆角矩形)
    stadium([体育场形])
    cylindrical[(圆柱形)]
    rhombus{菱形}
    parallelogram[/平行四边形/]
    trapezium[/梯形\]
    hexagon{{六边形}}
    ring(((圆环)))

    roundedRectangle-->stadium---cylindrical---|to rhombus|rhombus-.-parallelogram==>|to trapezium|trapezium~~~|hide line|hexagon--->ring

    a --> b & c--> d
    A & B--> C & D
```

## graph

```mermaid
graph LR
Dispatch_Action-->Reducer-->State-->Subscribe-->UI-->Dispatch_Action
```

## class

```mermaid
---
title: Animal example
---
classDiagram
    note "From Duck till Zebra"
    Animal <|-- Duck
    note for Duck "can fly\ncan swim\ncan dive\ncan help in debugging"
    Animal <|-- Fish
    Animal <|-- Zebra
    Animal : +int age
    Animal : +String gender
    Animal: +isMammal()
    Animal: +mate()
    class Duck{
        +String beakColor
        +swim()
        +quack()
    }
    class Fish{
        -int sizeInFeet
        -canEat()
    }
    class Zebra{
        +bool is_wild
        +run()
    }
```

## journey

```mermaid
journey
    title My working day
    section Go to work
      Make tea: 5: Me
      Go upstairs: 3: Me
      Do work: 1: Me, Cat
    section Go home
      Go downstairs: 5: Me
      Sit down: 5: Me
```

## gantt

```mermaid
gantt
    title A Gantt Diagram
    dateFormat YYYY-MM-DD
    section Section
        A task          :a1, 2014-01-01, 30d
        Another task    :after a1, 20d
    section Another
        Task in Another :2014-01-12, 12d
        another task    :24d
```

## pie

```mermaid
pie     
    showData
    title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
```

## quadrantChart

```mermaid
quadrantChart
    title Reach and engagement of campaigns
    x-axis Low Reach --> High Reach
    y-axis Low Engagement --> High Engagement
    quadrant-1 We should expand
    quadrant-2 Need to promote
    quadrant-3 Re-evaluate
    quadrant-4 May be improved
    Campaign A: [0.3, 0.6]
    Campaign B: [0.45, 0.23]
    Campaign C: [0.57, 0.69]
    Campaign D: [0.78, 0.34]
    Campaign E: [0.40, 0.34]
    Campaign F: [0.35, 0.78]
```

