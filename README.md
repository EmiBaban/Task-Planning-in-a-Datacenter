Tema #2 Planificarea de task-uri intr-un datacenter

Băban Mihai-Emilian, 334CD

MyDispatcher:

- este responsabil pentru asignarea task-urilor la diverse host-uri bazate pe diferite algoritme de planificare.

- algoritmi de planificare implementati:

Round Robin:

    - nodurile sunt planificate  (i + 1) % n, unde i este ID-ul ultimului nod la care s-a alocat un task,
    
     iar n este numarul total de noduri.


Shortest Queue:

    - parcuge lista de host-uri pentru a afla host-ul cu coada cea mai mica
    
    - daca exista un task in executie il adun la dimensiune
    
    - adauga task-ul la host-ul respectiv


Size Interval Task Assignment:

    - daca task-ul este short este adaugat host-ului 0, daca e medium este adaugat la 1,
    
    iar daca este long, este adaugat la 2



Least Work Left:

    - similar cu Shortest Queue doar ca se extrage host-ul cu durata totala cea mai mica de calcule ramase de executat



MyHost:

- este responsabil de executarea task-urilor

- am implementat clasa QueueComparator pentru coada de prioritate. Daca au prioritati egale compar dupa start

- getWorkLeft():

    - calculez durata totala a task-urilor din coada si apoi adun cu durata ramasa din task-ul ce e in executie

- extrag elementul cu prioritatea cea mai mare din coada si setez taskInExecution true

- cat timp timpul ramas al task-ului nu ajunge la 0, scad din left cat timp a trecut intr-o iteratie in loop

- daca task-ul care ruleaza e preemptabil si task-ul urmator are prioritate mai mare, task-ul cu prioritate mai mare

    devine cel care ruleaza, iar celalalt este adaugat inapoi in coada

- dupa ce s-a iesit din loop termin task-ul
