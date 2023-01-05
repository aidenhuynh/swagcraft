## Crafting recipes

<style>
    .gridrow {
        width:10%;
        margin-left:5px;
        margin-right:5px;
        text-align:center;
        border-left-width: 100%;
    }


</style>

<table>
    <tbody id="bruh">
    <tr>
        <th>Item</th>
        <th colspan="3">Recipe </th>
        <th colspan="3"></th>
        <th>Output</th>
    </tr>
    </tbody>
</table>

<script>
// For this, do "item_name":"image url"
var items = {
    "blank":"images/blank.png",
    "plank":"images/wooden_planks.webp",
    "stick":"images/stick.webp",
    "woodenSlab":"images/wooden_slab.webp"

}


// craftables Format:
// {
//     "itemName":
//     "ITEMHERE",

//     "itemRecipe":[
//     [items["blank"], items["blank"], items["blank"]],
//     [items["blank"], items["blank"], items["blank"]],
//     [items["blank"], items["blank"], items["blank"]]
//     ],

//     "itemOutput":
//     items["ITEMHERE"]
// },

var craftables = [
{
    "itemName":
    "Stick",

    "itemRecipe":[
    [items["blank"], items["blank"], items["blank"]],
    [items["blank"], items["plank"], items["blank"]],
    [items["blank"], items["plank"], items["blank"]]
    ],

    "itemOutput":
    items["stick"]
},
{
    "itemName":
    "Wooden Slab",

    "itemRecipe":[
    [items["blank"], items["blank"], items["blank"]],
    [items["plank"], items["plank"], items["plank"]],
    [items["blank"], items["blank"], items["blank"]]
    ],

    "itemOutput":
    items["woodenSlab"]
},

]

for (let i = 0; i < craftables.length; i++) {
    document.getElementById('bruh').innerHTML += '\
    <tr> \
        <td rowspan="3">' + craftables[i]["itemName"] + '</td> \
        \
        <td class="gridrow"><img src="' + craftables[i]["itemRecipe"][0][0] + '"style="width:30px;height:30px;"></td> \
        <td class="gridrow"><img src="' + craftables[i]["itemRecipe"][0][1] + '"style="width:30px;height:30px;"></td> \
        <td class="gridrow"><img src="' + craftables[i]["itemRecipe"][0][2] + '"style="width:30px;height:30px;"></td> \
        \
        <td rowspan="3" colspan="3" style="text-align:center"><img src="images/right_arrow_temp.png" style="width:80px;height:50px"></td> \
        <td rowspan="3"><img src="' + craftables[i]["itemOutput"] + '"style="width:50px;height:50px;"></td> \
    </tr> \
    <tr> \
        <td class="gridrow"><img src="' + craftables[i]["itemRecipe"][1][0] + '"style="width:30px;height:30px;"></td> \
        <td class="gridrow"><img src="' + craftables[i]["itemRecipe"][1][1] + '"style="width:30px;height:30px;"></td> \
        <td class="gridrow"><img src="' + craftables[i]["itemRecipe"][1][2] + '"style="width:30px;height:30px;"></td> \
    </tr> \
    <tr> \
        <td class="gridrow"><img src="' + craftables[i]["itemRecipe"][2][0] + '"style="width:30px;height:30px;"></td> \
        <td class="gridrow"><img src="' + craftables[i]["itemRecipe"][2][1] + '"style="width:30px;height:30px;"></td> \
        <td class="gridrow"><img src="' + craftables[i]["itemRecipe"][2][2] + '"style="width:30px;height:30px;"></td> \
    </tr> \
    '
  }


</script>