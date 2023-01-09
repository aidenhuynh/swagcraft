<style>
    td {
        table-layout:fixed;
        padding:5px 10px;
    }

    .gridrow {
        width:30px;
        height:30px;
        text-align:center;
        border: 1px solid #434343; /* I tried to use sass here but it didn't work :( */
        border-top: 1px solid #434343;
        border-bottom: 1px solid #434343;
        padding:5px 5px;

    }

    .outputtd {
        width:auto
    }

    input {
        color: #434343;
        border: 0px;
        margin-left: 2%;
        width: 80%;
        white-space: nowrap
    }
</style>

## Crafting Recipes
<label for="searchBar"> Search: <input name="searchBar" id="searchBar" placeholder="Enter item name here"></label>

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

var items = {
    "blank":
    {
        "imageURL":"images/blank.png",
        "itemName":"Nothing"
        },

    "log":
    {
        "imageURL":"images/log.webp",
        "itemName":"Log"
        },

    "plank":
    {
        "imageURL":"images/wooden_planks.webp",
        "itemName":"Wooden Planks"
        },

    "stick":
    {
        "imageURL":"images/stick.webp",
        "itemName":"Stick"
        },

    "woodenSlab":
    {
        "imageURL":"images/wooden_slab.webp",
        "itemName":"Wooden Slab"
        },
    "woodenPickaxe":
    {
        "imageURL":"images/wooden_pickaxe.webp",
        "itemName":"Wooden Pickaxe"
    },
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
//     items["ITEMHERE"],

//     "itemQuantity":
//     QUANTITY
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
    items["stick"],

    "itemQuantity":
    4
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
    items["woodenSlab"],

    "itemQuantity":
    3
},
{
    "itemName":
    "Wooden Planks",

    "itemRecipe":[
    [items["blank"], items["blank"], items["blank"]],
    [items["blank"], items["log"], items["blank"]],
    [items["blank"], items["blank"], items["blank"]]
    ],

    "itemOutput":
    items["plank"],

    "itemQuantity":
    4
},
{
    "itemName":
    "Wooden Pickaxe",

    "itemRecipe":[
    [items["plank"], items["plank"], items["plank"]],
    [items["blank"], items["stick"], items["blank"]],
    [items["blank"], items["stick"], items["blank"]]
    ],

    "itemOutput":
    items["woodenPickaxe"],

    "itemQuantity":
    1
},
]

function createRow(list, index, rowNum) {
    n = 0
    output = ""

    while (n < 3) {
        output += ' \
        <td class="gridrow"><img title="' + list[index]["itemRecipe"][rowNum][n]["itemName"] + '" src="' + list[index]["itemRecipe"][rowNum][n]["imageURL"] + '"style="width:30px;height:30px;"></td> \
        '
        n += 1
    }
    
    return output
}

function getRecipes(list) {
    document.getElementById('bruh').innerHTML = " \
    <tr> \
        <th>Item</th> \
        <th colspan='3'>Recipe </th> \
        <th colspan='3'></th> \
        <th>Output</th> \
    </tr> \
    "

    for (let i = 0; i < list.length; i++) {
        document.getElementById('bruh').innerHTML += '\
        <tr> \
            <td rowspan="3">' + list[i]["itemName"] + '</td> \
             \
            ' + createRow(list, i, 0) + ' \
             \
            <td rowspan="3" colspan="3" style="text-align:center"><img src="images/right_arrow.png" style="width:80px;height:30px"></td> \
            <td rowspan="3" style="width:50px"><img title="' + list[i]["itemOutput"]["itemName"]+ ' "src="' + list[i]["itemOutput"]["imageURL"] + '"style="wrapping:none;width:auto;height:auto;">\n <i style="text-align:right">' + list[i]["itemQuantity"] + '</i></td> \
        </tr> \
        <tr>\n' + createRow(list, i, 1) + '\n</tr> \
        <tr>\n' + createRow(list, i, 2) + '\n</tr> \
        '
    }
}

function search(list) {
    
    
    results = []
    input = document.getElementById('searchBar').value.toLowerCase()

    if (input == "" || input == null) {
        getRecipes(craftables)
    }
    else {
        for (let i = 0; i < list.length; i++) {
            item = list[i]["itemName"].toLowerCase()

            if (item.includes(input) == true) {
                results.push(list[i])
            }
        }
        if (results.length == 0) {
            document.getElementById('bruh').innerHTML = "\
            <tr> \
            <th>Item</th> \
            <th colspan='3'>Recipe </th> \
            <th colspan='3'></th> \
            <th>Output</th> \
            </tr> \
            <tr><td colspan='8'><i>No results found.</i></td></tr> \
            "
        }
        else {
        getRecipes(results)
        }
    }
}

searchBar.addEventListener("keyup", function() {
            search(craftables)
        }
    )

getRecipes(craftables)
</script>