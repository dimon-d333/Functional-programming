# Functional-programming

**1. Запишите последовательности вызовов CAR и CDR, выделяющие из приведенных ниже списков символ цели. Упростите эти вызовы с помощью комбинации селекторов:
• (1 2 цель 3 4)
• ((1) (2 цель) (3 (4)))
• ((1 (2 (3 4 цель))))**
```lisp
(print (caddr '(1 2 цель 3 4)))
(print (cadadr '((1) (2 цель) (3 (4)))))
(print (caddar (cdadar  '((1 (2 (3 4 цель)))))))
```
**7. Определите функцию, удаляющую из исходного списка элементы с четными номерами.**
```lisp
(defun delete-even-num (w) 
    (cond
         ((null w) nil) 
         (t (cons (car w) (delete-even-num (cddr w))))
    )
) 
 
(print (delete-even-num '(1 2 3 4 5 6))); (1 3 5)
(print (delete-even-num '(1)));(1)
(print (delete-even-num '(a b c d)));(A C)
```

**10. Определите функцию, осуществляющую удаление указанного количества последних элементов исходного списка.**
```lisp
(defun delete-last-el (list n) 
    (cond
         ((= (list-length  list) n) nil) 
         (t (cons (car list) (delete-last-el (cdr list) n)))
    )
) 
 
(print (delete-last-el '(1 2) 2)) ;NIL
(print (delete-last-el '(a b 3 4 5) 3)) ;(A B)
(print (delete-last-el '(1 2) 0)) ;(1 2)
```
**15. Определите функцию, вычисляющую скалярное произведение векторов, заданных списками целых чисел.**
```lisp
(defun scalar-product (list1 list2) 
   ( (lambda (first-list1 first-list2 rest-list1 rest-list2)
        (cond
             ((null list1) 0) 
             (t (+ (* first-list1 first-list2) (scalar-product rest-list1 rest-list2 )) )
        )
     ) (car list1)(car list2)(cdr list1)(cdr list2) ) 
) 
    
(print (scalar-product '(1 2 3) '(1 2 3))) ;14
(print (scalar-product '(5) '(5))) ;25
(print (scalar-product '(6 3) '(1 1))) ;9
```
**20. Определите функцию ПЕРВЫЙ-АТОМ, результатом которой будет первый атом списка**
```lisp
(defun первый-атом (list) 
  ( ( lambda (first)
             (cond 
                 ((atom first) first)
                 (t (первый-атом first))
              )
    )(car list)
  )    
) 
    
(print (первый-атом '(((a b)) c d)) ) ;A
(print (первый-атом '((((1 ) b)) c d)) ) ;1
(print (первый-атом '(((atom) a) b) ) ) ;ATOM
```
**26. Определите функцию, разбивающую список (a b с d...) на пары ((а b) (с d)...).**
```lisp
(defun pair(list)
    (( lambda (first second rest )
               ( cond
                   ((null rest)  (cons (list first second ) rest) ) 
                   (t (cons (list first second ) (pair rest)) )
               )   
      ) (car list) (cadr list) (cddr list))
)

(print ( pair '(a b c d))) ;((A B) (C D))
(print ( pair '(a b) ) ) ; ((A B))
(print ( pair '(a b c d e f) ) ) ; ((A B) (C D) (E F))
```
**39. Определите функцию СИММЕТРИЧЕСКАЯ-РАЗНОСТЬ, формирующую множество из элементов не входящих в оба множества.**
```lisp
(defun поиск (list1 list2)
    (cond 
        ((null list1) nil)
        ((member (car list1) list2) (поиск (cdr list1) list2))
        (t (cons (car list1) (поиск (cdr list1) list2) ))
        
    )
)

(defun симметрическая-разность (list1 list2)
     (append (поиск list1 list2) (поиск list2 list1))
)

(print ( симметрическая-разность '(1 2 3) '(3 4 5 6)) ) ;(1 2 4 5 6)
(print (симметрическая-разность '(a b c d) '(c a b)) ) ;(d)
(print (симметрическая-разность '(a b) '(c d)) ) ;(a b c d)
```
**32. Определите предикат МНОЖЕСТВО-Р, который проверяет, является ли список множеством, т.е. входит ли каждый элемент в список лишь один раз.**
```lisp
(defun множество-р(list)
    (( lambda( first rest )
               ( cond
                   ((null list) t )
                   ((member first rest) nil )
                   (t (множество-р rest) )
               )   
      ) (car list) (cdr list))
)

(print (множество-р '(a b c d))); T - множество
(print (множество-р '(a b c d a))); NIL - не множество
(print (множество-р '())); T – множество
```
**42. Определите функцию, находящую максимальное из значений, находящихся в вершинах дерева.**
```lisp
(defun max-elem (tree) (
    cond 
        ((null (first tree)) -1)
        ((not (or (second tree) (third tree))) (first tree))
        (t (max (max-elem (second tree)) (max-elem (third tree))))))


(print (max-elem '(1 (2 (6) ()) (3 () (10)))));10
```
**47. Определите функцию УДАЛИТЬ-ВСЕ-СВОЙСТВА, которая удаляет все свойства символа.**
```lisp
(defun удалить-все-свойства(x)
    ( (lambda (свойства)
         ( cond 
             ((null свойства ) t )
             (t (remprop x (car свойства)) (удалить-все-свойства x))
         )
    )(SYMBOL-PLIST x))
)

(setf (get 'x 'property1)'value)
(setf (get 'x 'property2)2)

(удалить-все-свойства 'x)
```
