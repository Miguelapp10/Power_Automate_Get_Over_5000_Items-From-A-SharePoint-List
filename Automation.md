A continuacion le mostrare el flujo que elabore:

*RECURRENCE*

<img width="553" height="330" alt="image" src="https://github.com/user-attachments/assets/ece349b5-de2a-4635-adcb-9223f7d54ef3" />

* Initialize variable: varListItems*

<img width="564" height="306" alt="image" src="https://github.com/user-attachments/assets/d5a0e485-4fbb-4603-9d5a-46dfa1aac838" />

*Initialize variable: varSharePointUri*

<img width="566" height="361" alt="image" src="https://github.com/user-attachments/assets/9a83e1e2-1a41-45d1-b67f-90f7409134cc" />

`_api/web/lists/GetByTitle('Devoluciones Linio.com')/items?$select=ID,Title,Fecharetorno3,TiendaDev3,Unidades3,Empresa3,Folio3,Placa3,Registro3,Estado3,PEDIDODANADO3&$filter=ID gt 9000&$top=5000`

* Do - Do Until*
  
<img width="301" height="516" alt="image" src="https://github.com/user-attachments/assets/ab9e0516-480b-4823-bea9-7b8b8f42350b" />

*Send an HTTP request to SharePoint*

<img width="552" height="471" alt="image" src="https://github.com/user-attachments/assets/decd799e-da7b-452e-9b3c-ae696d9a4df0" />

*Parse JSON: List items*

<img width="549" height="556" alt="image" src="https://github.com/user-attachments/assets/0ad723a3-3df0-42d6-b6f7-91a50358a950" />

*Compose: All List Items*

<img width="557" height="175" alt="image" src="https://github.com/user-attachments/assets/8c88239c-784f-40d6-8fca-d776dff9872f" />

`if(
  equals(
    empty(variables('varListItems')),
    true
  ),
  body('Parse_JSON:_List_items')?['d']?['results'],
  union(
    variables('varListItems'),body('Parse_JSON:_List_items')?['d']?['results']
  )
)`

*Set variable: varListItems*

<img width="565" height="258" alt="image" src="https://github.com/user-attachments/assets/e125e4b6-9f83-4ca7-b6f4-8e6572bfd0ca" />

`outputs('Compose:_All_List_Items')`

*Set variable*

<img width="561" height="238" alt="image" src="https://github.com/user-attachments/assets/056cedbb-60c3-4efe-bb6e-868c3e964d1b" />

`if(
  equals(
    body('Parse_JSON:_List_Items')?['d']?['__next'],
    null
  ),
  '',
  last(
      split(
        body('Parse_JSON:_List_Items')?['d']?['__next'],
        'sincorreo2/'
      )
  )
)`

*Do until*

<img width="551" height="432" alt="image" src="https://github.com/user-attachments/assets/75e11941-d903-419d-8087-01df0c5455b4" />

`variables('varSharePointUri') is equal to string('')`

*Select*

<img width="553" height="489" alt="image" src="https://github.com/user-attachments/assets/c39f8d53-c101-4fe5-bef0-6bb33ec4ad97" />

`outputs('Compose:_All_List_Items')`

*Create CSV table*

<img width="557" height="280" alt="image" src="https://github.com/user-attachments/assets/41b22e05-ba45-4812-bacc-086f1365ca0a" />

`body('Select')`

*Update file*

<img width="560" height="307" alt="image" src="https://github.com/user-attachments/assets/c6a574dd-fd85-46b4-a0d8-70baa4ea6f3f" />

`body('Create_CSV_table')`

*Flujo Final*

<img width="96" height="556" alt="image" src="https://github.com/user-attachments/assets/c49e5f69-7e9a-44e8-b7c6-1642253af576" />

