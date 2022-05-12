<script>
export default {
    data() {
        return {
            input_value: '',
            name: '',
            firstname: 'Bishwas',
            lastname: 'Dangol',
            food_items: [
                {
                    "foodName": "Pizza",
                },
                {
                    "foodName": "MoMo",
                }
            ],
            myObject: {
                name: "Bishwas Dangol",
                location: "Kathmandu"
            },
        };
    },
    // we only use computed properties if want to call a method in the HTML code.
    // cause vue does not identify which method we want of execute as if we call none method 
    // it will defaultly execute the othe methods as well in the background.
    computed: {
        fullname() {
            if (this.name === ""){
                return ""
            }
            return this.name+" "+'Dangol'
        },
        realFullname: {
            get () {
                return this.firstname + " " + this.lastname
            },
            set (newValue) {
                [this.firstname, this.lastname] = newValue.split(" ")
            }
        }
    },
    methods: {
        inputHandler(event) {
            this.input_value = event.target.value
        },
        submitHandler() {
            this.name = this.input_value
            this.input_value = ""
        },
        resetInput() {
            this.name = ""
        },
        removeItem(index) {
            this.food_items.splice(index, 1)
        }
    },
    mounted() {
        setTimeout(() => {
            this.firstname = "Priya"
        }, 2000)
    },
}
</script>
<!--v-on:keyup.enter="submitHandler" (for submitting the form by any keyboard key)-->
<!--v-model="name" for two way binding instead of v-on:input="inputHandler"v-bind:value="input_value"-->
<template>
    <div id="container">
        <form id="form-container" v-on:submit.prevent="">
            <input 
                type="text" 
                placeholder="Say any thing..."
                v-model="input_value">
            <button 
                v-on:click="submitHandler">
                Submit
            </button>
            <button
                v-on:click="resetInput">
                Reset
            </button>
        </form>
        <br />
        <p>{{ name }}</p>
        <br />
        <p>{{ realFullname }}</p>
        <p v-if="food_items.length === 0">
            We don't have any thing on the list !!!
        </p>
        <ul v-else>
            <!-- we should always use :key(v-bind:key) to uniquely identify the item when using v-for-->
            <li v-for="(food, index) in food_items" @click="removeItem(index)" :key="food">
                <p>{{ food.foodName }} - {{ index }}</p>
                <input type="text" @click.stop>
            </li>
            <!--use of destructuring on the v-for-->
            <!-- <li v-for="{ foodName } in food_items">{{ foodName }}</li> -->
            <!--v-for in objects-->
            <!--we can also use of instead of in lin v-for loop-->
            <!-- <li v-for="value of myObject">
                {{ value }}
            </li> -->
            <!-- <li v-for="(value, key, index) in myObject">
               {{ index }}. {{ key }}: {{ value }}
            </li> -->
        </ul>
    </div>
</template>