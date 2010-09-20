!SLIDE

##  
##  
##  
##  

# Symbolic Functional Decomposition Method<br />for Implementation of Finite State Machines<br />in FPGA Devices

<h2 style='font-size: 2.1em;'>Piotr Szotkowski</h2>

##  

## promotor: prof. dr hab. inż. Tadeusz Łuba



!SLIDE

# symboliczna dekompozycja funkcjonalna

<div style='height: 3em;'></div>

![dekompozycja](symbolic.png)



!SLIDE

# częściowe kodowanie stanów

<table class='lay'>
  <tr>
    <td>
      <table class='fsm state'>
        <thead>
          <tr><th>X</th><th>Q</th><th></th><th>Q’</th><th>Y</th></tr>
        </thead>
        <tbody>
          <tr><td>–   –   0   0</td><td>init0 </td><td></td><td>init1 </td><td>0   0</td></tr>
          <tr><td>0   1   0   0</td><td>init1 </td><td></td><td>init1 </td><td>0   0</td></tr>
          <tr><td>–   –   1   –</td><td>init1 </td><td></td><td>init2 </td><td>1   0</td></tr>
          <tr><td>1   –   1   0</td><td>init2 </td><td></td><td>init4 </td><td>1   0</td></tr>
          <tr><td>–   1   1   1</td><td>init4 </td><td></td><td>init4 </td><td>1   0</td></tr>
          <tr><td>–   –   0   1</td><td>init4 </td><td></td><td>IOwait</td><td>0   1</td></tr>
          <tr><td>0   0   0   –</td><td>IOwait</td><td></td><td>IOwait</td><td>0   1</td></tr>
          <tr><td>1   0   0   –</td><td>IOwait</td><td></td><td>init1 </td><td>0   1</td></tr>
          <tr><td>0   1   1   0</td><td>IOwait</td><td></td><td>read0 </td><td>0   0</td></tr>
          <tr><td>1   1   0   0</td><td>IOwait</td><td></td><td>write0</td><td>1   1</td></tr>
          <tr><td>0   1   1   1</td><td>IOwait</td><td></td><td>RMACK </td><td>1   1</td></tr>
          <tr><td>1   1   0   1</td><td>IOwait</td><td></td><td>WMACK </td><td>0   0</td></tr>
          <tr><td>–   0   1   –</td><td>IOwait</td><td></td><td>init2 </td><td>0   1</td></tr>
          <tr><td>0   0   1   0</td><td>RMACK </td><td></td><td>RMACK </td><td>1   1</td></tr>
          <tr><td>0   1   1   1</td><td>RMACK </td><td></td><td>read0 </td><td>0   0</td></tr>
          <tr><td>1   1   0   0</td><td>WMACK </td><td></td><td>WMACK </td><td>0   0</td></tr>
          <tr><td>1   0   0   1</td><td>WMACK </td><td></td><td>write0</td><td>0   1</td></tr>
          <tr><td>0   0   0   1</td><td>read0 </td><td></td><td>read1 </td><td>1   1</td></tr>
          <tr><td>0   0   1   0</td><td>read1 </td><td></td><td>IOwait</td><td>0   1</td></tr>
          <tr><td>0   1   0   0</td><td>write0</td><td></td><td>IOwait</td><td>0   1</td></tr>
        </tbody>
      </table>
    </td>
    <td>
      <table class='fsm state encoded'>
        <thead>
          <tr><th>X</th><th>Q<sub>U</sub></th><th>Q<sub>V</sub></th><th></th><th>Q’<sub>U</sub></th><th>Q’<sub>V</sub></th><th>Y</th></tr>
        </thead>
        <tbody>
          <tr><td>–   –   0   0</td><td>u<sub>1</sub></td><td>v<sub>1</sub></td><td></td><td>u<sub>1</sub></td><td>v<sub>2</sub></td><td>0   0</td></tr>
          <tr><td>0   1   0   0</td><td>u<sub>1</sub></td><td>v<sub>2</sub></td><td></td><td>u<sub>1</sub></td><td>v<sub>2</sub></td><td>0   0</td></tr>
          <tr><td>–   –   1   –</td><td>u<sub>1</sub></td><td>v<sub>2</sub></td><td></td><td>u<sub>2</sub></td><td>v<sub>3</sub></td><td>1   0</td></tr>
          <tr><td>1   –   1   0</td><td>u<sub>2</sub></td><td>v<sub>3</sub></td><td></td><td>u<sub>2</sub></td><td>v<sub>3</sub></td><td>1   0</td></tr>
          <tr><td>–   1   1   1</td><td>u<sub>2</sub></td><td>v<sub>3</sub></td><td></td><td>u<sub>2</sub></td><td>v<sub>3</sub></td><td>1   0</td></tr>
          <tr><td>–   –   0   1</td><td>u<sub>2</sub></td><td>v<sub>3</sub></td><td></td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td>0   1</td></tr>
          <tr><td>0   0   0   –</td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td></td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td>0   1</td></tr>
          <tr><td>1   0   0   –</td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td></td><td>u<sub>1</sub></td><td>v<sub>2</sub></td><td>0   1</td></tr>
          <tr><td>0   1   1   0</td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td></td><td>u<sub>2</sub></td><td>v<sub>2</sub></td><td>0   0</td></tr>
          <tr><td>1   1   0   0</td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td></td><td>u<sub>2</sub></td><td>v<sub>3</sub></td><td>1   1</td></tr>
          <tr><td>0   1   1   1</td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td></td><td>u<sub>4</sub></td><td>v<sub>2</sub></td><td>1   1</td></tr>
          <tr><td>1   1   0   1</td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td></td><td>u<sub>4</sub></td><td>v<sub>3</sub></td><td>0   0</td></tr>
          <tr><td>–   0   1   –</td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td></td><td>u<sub>2</sub></td><td>v<sub>3</sub></td><td>0   1</td></tr>
          <tr><td>0   0   1   0</td><td>u<sub>4</sub></td><td>v<sub>2</sub></td><td></td><td>u<sub>4</sub></td><td>v<sub>2</sub></td><td>1   1</td></tr>
          <tr><td>0   1   1   1</td><td>u<sub>4</sub></td><td>v<sub>2</sub></td><td></td><td>u<sub>2</sub></td><td>v<sub>2</sub></td><td>0   0</td></tr>
          <tr><td>1   1   0   0</td><td>u<sub>4</sub></td><td>v<sub>3</sub></td><td></td><td>u<sub>4</sub></td><td>v<sub>3</sub></td><td>0   0</td></tr>
          <tr><td>1   0   0   1</td><td>u<sub>4</sub></td><td>v<sub>3</sub></td><td></td><td>u<sub>2</sub></td><td>v<sub>3</sub></td><td>0   1</td></tr>
          <tr><td>0   0   0   1</td><td>u<sub>2</sub></td><td>v<sub>2</sub></td><td></td><td>u<sub>2</sub></td><td>v<sub>1</sub></td><td>1   1</td></tr>
          <tr><td>0   0   1   0</td><td>u<sub>2</sub></td><td>v<sub>1</sub></td><td></td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td>0   1</td></tr>
          <tr><td>0   1   0   0</td><td>u<sub>2</sub></td><td>v<sub>3</sub></td><td></td><td>u<sub>3</sub></td><td>v<sub>1</sub></td><td>0   1</td></tr>
        </tbody>
      </table>
    </td>
  </tr>
</table>



!SLIDE

# złożoność

## **dobór U i V**
## wyczerpujący: O(2<sup>|X|</sup>)
## ogólnej istotności wejść<br />i unikalności dostarczanej informacji: O(2<sup>|seq|</sup>)

## **konstrukcja β<sub>Q<sub>U</sub></sub>**
## <i>r</i>-przydatność: O(|β<sub>Q</sub>|<sup>2</sup> · |β<sub>U</sub>|)
## łączenie wierzchołków grafu: O(|β<sub>Q</sub>|)<sup>2</sup> · log<sub>2</sub>|β<sub>Q</sub>|)

## **konstrukcja β<sub>G</sub> i β<sub>Q<sub>V</sub></sub>**
## kolorowanie grafu niezgodności: O(|β|<sup>2</sup> · |S|)
## łączenie wierzchołków grafu: O(|β|<sup>2</sup> · |S|)
## kolorowanie równoległe: O(|β<sub>Q</sub> • β<sub>V</sub>|<sup>2</sup> · |S| + |β<sub>Q</sub> • S<sub>V</sub>|<sup>4</sup>)
