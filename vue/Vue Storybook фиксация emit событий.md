```javascript
//import-ы компонентов и данных
import TargetComponent from ".."
import { TargetComponentData }  from ".."


//внутри компонента ставим $emit('fire')

export default {
    title: 'TargetComponent',
    component: TargetComponent,
    argTypes: { click: { action: 'clicked' } }, //специально обрабатываем всплывающее из компонента событие
};

const Template = (args, { argTypes }) => ({
    components: { TargetComponent },
    props: Object.keys(argTypes),
    template: `<target-component @fire="click"/>` //добавляем аргумент чтобы ловить всплывающее событие
});

export const primary = Template.bind({});

primary.args = {
    card: TargetComponentData
};
```


#vue #storybook