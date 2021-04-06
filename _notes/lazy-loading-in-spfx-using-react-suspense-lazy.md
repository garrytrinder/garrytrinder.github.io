# Code splitting and dynamic loading of components in SPFx using React Suspense and React Lazy

Optimise bundle size, load in components only when required.

Reference Script Editor webpart by Mikael Svensson

```js
const editorPropImport = await import(
      /* webpackChunkName: 'plre-list-viewer' */
      '@pnp/spfx-property-controls/lib/PropertyFieldCodeEditor'
    );

return {
    ...,
    groupFields: [
        editorProp.PropertyFieldCodeEditor('htmlCode', {
            label: 'Handlebars Template',
            panelTitle: 'Edit Handlebars Template',
            initialValue: this.properties.htmlCode,
            onPropertyChange: this.onPropertyPaneFieldChanged.bind(this),
            properties: this.properties,
            disabled: false,
            key: 'htmlCode',
            language: editorProp.PropertyFieldCodeEditorLanguages.Handlebars,
            }),
        ...
}
```

webpackChunkName comment ensures that the split file is named with a vendor prefix for easy identification

Dynamically load a PnP component

```js
const Placeholder = React.lazy(() => import(/* webpackChunkName: 'plre-list-viewer' */ './pnp/Placeholder'));
```

Requires the component to be the default export so we have to use middle-man module to import from PnP and export as default

```js
import { Placeholder } from '@pnp/spfx-controls-react/lib/Placeholder';

export default Placeholder;
```
