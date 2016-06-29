# [1/6]  Level 1: Hello, world of XSS

##Mission Description

This level demonstrates a common cause of cross-site scripting where user input is directly included in the page without proper escaping. 

Interact with the vulnerable application window below and find a way to make it execute JavaScript of your choosing. You can take actions inside the vulnerable window or directly edit its URL bar.

##Mission Objective

Inject a script to pop up a JavaScript alert() in the frame below. 

Once you show the alert you will be able to advance to the next level.

## Write Up Iker

El objetivo de este nivel consiste en ejecutar una alerta en el navegador insertando código en el Textarea que nos proporciona.

Escribimos un script básico como el siguiente y lo introducimos en el campo y pulsamos **SEARCH**:

```javascript
<script>alert('aibalaostiapues!')</script>
```

El texto introducido en el textarea se ejecuta como una alerta en el navegador y nos muestra un mensaje diciendo que hemos pasado la prueba. :)
