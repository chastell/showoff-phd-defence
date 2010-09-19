!SLIDE

# automat skończony

<table class='lay'>
  <tr>
    <td>
      <table class='fsm'>
        <thead>
          <tr><th>wejście</th><th>stan akt.</th><th></th><th>stan nast.</th><th>wyjście</th></tr>
        </thead>
        <tbody>
          <tr><td>zasuń</td><td>odsunięte</td><td></td><td>zasunięte</td><td>zasuwanie</td></tr>
          <tr><td>zamknij</td><td>zasunięte</td><td></td><td>zamknięte</td><td>zamykanie</td></tr>
          <tr><td>otwórz</td><td>zamknięte</td><td></td><td>zasunięte</td><td>otwieranie</td></tr>
          <tr><td>odsuń</td><td>zasunięte</td><td></td><td>odsunięte</td><td>odsuwanie</td></tr>
        </tbody>
        <tbody>
          <tr style='height: 2em;'></tr>
        </tbody>
        <thead>
          <tr><th>X</th><th>Q</th><th></th><th>Q’</th><th>Y</th></tr>
        </thead>
        <tbody>
          <tr><td>0     0</td><td>odsunięte</td><td></td><td>zasunięte</td><td>0     0</td></tr>
          <tr><td>0     1</td><td>zasunięte</td><td></td><td>zamknięte</td><td>0     1</td></tr>
          <tr><td>1     0</td><td>zamknięte</td><td></td><td>zasunięte</td><td>1     0</td></tr>
          <tr><td>1     1</td><td>zasunięte</td><td></td><td>odsunięte</td><td>1     1</td></tr>
        </tbody>
      </table>
    </td>
    <td>
      <p><img src='image/fsm/fsm.graph.png' /></p>
      <p style='height: 2em;'></p>
      <p><img src='image/fsm/fsm.schema.png' /></p>
    </td>
  </tr>
</table>
