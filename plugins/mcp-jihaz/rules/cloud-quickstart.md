# Лаборатория через облачный MCP

Типовая Г-кухня: `generate_furniture({spec, positionId, verbose:false})`.
Для простого эскиза — бриф `kind:'kitchen'`, две `walls` с `sections`.
`build_furniture` — внутренний обработчик, скрытый из каталога MCP.
Готовый JSON: `get_agent_kit({path:'recipes/corner-kitchen.json'})`.
Сначала `get_lab_session({positionId})`: не потеряйте модель и правки технолога.
Спецификация `kind:'cornerKitchen'`:

```json
{
  "kind":"cornerKitchen", "revision":1,
  "walls":[{"name":"Стена A","length":3100},{"name":"Стена B","length":2100}],
  "height":2900, "ceilingFiller":100, "backsplash":600,
  "countertop":{"thickness":38}, "plinth":{"recess":50},
  "corner":{"joint":{"node":"bottomSink","width":600}},
  "upperCorner":{},
  "branches":[
    {"name":"A","modules":[
      {"name":"А1","node":"bottomBox","width":"auto","minWidth":300},
      {"name":"Варочная","node":"bottomDrawers","width":600},
      {"name":"А3","node":"bottomBox","width":"auto","minWidth":300}],
     "tail":[{"name":"Техника","node":"penalAppliance","width":600,"mainHeight":2200}],
     "upper":[{"name":"В1","node":"topBox","width":"auto"},
       {"name":"Вытяжка","node":"hoodBox","width":600},
       {"name":"В3","node":"topBox","width":"auto"}]},
    {"name":"B","modules":[{"name":"Ящики","node":"bottomDrawers","width":"auto","minWidth":250}],
     "tail":[{"name":"Пенал","node":"penal","width":600,"mainHeight":2200}],
     "upper":[{"name":"В4","node":"topBox","width":"auto"}]}
  ]
}
```

Две стены перпендикулярны. Первая — за глухим коробом, вторая — за стыковочным.
Мойка в углу — это `corner.joint.node: bottomSink`; отдельная мойка в `modules`
занимает ещё одну ширину. `auto` делит свободный остаток поровну. Фиксированные
размеры не растягиваются. `minWidth` запрещает непригодный узкий модуль.
`tail` резервируется до рабочих рядов; столешница останавливается перед пеналом.
`mainHeight` — верх основного пенала от пола; выше сервер ставит антресоль.
`opts` — параметры узла. Для приборов нужны паспортные ниши; пример не означает
готовность к производству. Вырезы мойки/варочной здесь не создаются.

Для нестандартного изделия — `run_lab_script`. Справочник узлов: `describe_nodes`.
`kit.roomFromSpec({revision:1,walls:[{name:'Стена A',length:3100,height:2900},
{name:'Стена B',length:2100,height:2900}],rows:[]})` строит стены.
Оси: Y вверх; X/Z — план. `vertical`: length по Y, width по Z, толщина по X.
`frontal`: length по X, width по Y. `horizontal`: length по X, width по Z.
`kit.place(node,{at,rotate})`: at.x/z — минимум габарита, at.y — сдвиг от узла.
rotate 0/180: ширина по X; 90/270: по Z; фасад +Z/+X/−Z/−X соответственно.
`kit.corner({tier:'top',between:[A,B],on:{row:low,backsplash:600}})` поднимает угол.
`kit.row({from:previousRow,...})` продолжает направление ряда; массив деталей
его не хранит. `alignFront:true` подбирает глубину, если `depth` не задан.
У ручных targets по повёрнутому модулю задайте `widthAxis:'z'`;
`worldSizeX/worldSizeZ` — мировые габариты. Спецификация выбирает ось сама.

`verbose:false`: пересечения по парам модулей и один кадр; проверки не отключаются.
`verbose:true`: все детали нарушений и кадры. Читайте alerts, targets и warnings.
Тулы `open_lab_project`, `save_lab_project`, `attach_model` — только десктоп.
Если `build_furniture` отсутствует у клиента, а `kit_doctor` его видит,
обновите каталог подключения MCP; не тратьте прогоны на поиск API.
