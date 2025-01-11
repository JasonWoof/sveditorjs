## sveditorjs v2

sveditorjs can be embed into any svelte or sveltekit project. It is a wrapper around editor.js for block editing that outputs clean json document.json that can be consumed by any app.

on version we added support for sveltekit
and added a utility helper 
that generates html

## docs and example
see the docs and example here [sveditorjs](https://sveditorjs.vercel.app):

```bash
npm install --save sveditorjs
```
```js
<script>
  import Editor ,{genHtml} from "$lib/index.js"; 
  
  let modes = {
          'js': 'JavaScript',
          'py': 'Python',
          'go': 'Go',
          'cpp': 'C++',
          'cs': 'C#',
          'md': 'Markdown',
        }
    let data = {}; //correct editorjs json data
    let urls = {} //this object should be 
    //{
      upload:"",
      load:"",
    }
 async function handleChange(ev){
    console.log(ev.detail) 
    let editor = ev.detail.editor;
    editor.save().then(async (savedData)=>{
      // do something with data
      console.log(window.current_sveditor); 
    // use helper to gen html
    let html = await genHtml(savedData);  
    console.log(html);
    }).catch((err)=>{console.log(err)})
  }
</script>

<Editor data={data} urls={urls} modes={modes} top="true" aside="true" on:editor_ready={(ev)=>{console.log("ready",ev.detail)}} on:editor_change ={(ev)=>{handleChange(ev)}} >
  <svelte:fragment slot="top" >
    top
  </svelte:fragment>
  <svelte:fragment slot="aside" >
   aside
  </svelte:fragment>
<svelte:fragment slot="extra" >
   extra unstyled
  </svelte:fragment>
</Editor>

 
```
