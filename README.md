

# Bitcoin Price Rates

## Project setup and launch
```
npm install
npm run serve
The project is also accessible on 
```

### Technologies and libraries used
```
Vue.js 2 (Vue CLI 3)
Bootstrap and FontAwesome
Bootstrap-Vue (Only for dropdown as Bootstrap Jquery intercepts with Vue)
FireBase (deployment)
```
### Possible improvements

*The way I track which currencies are displayed is hacky and could use a rework.
On receiving API Json data, current data into temp object (as new received data overwrites it) and by using Code, 
I move Display flags to a new object. There must be a cleaner way to do this.

*Also, I struggled to get Unicodes to work in <input> tags. 'V-model' attribute in <Input> does not support html.
Posible solution uwould be to use Vue computed properties in v-html tag (dont know if this going to work)

*Styling could also be added.




