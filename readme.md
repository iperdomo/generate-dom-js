## Generate DOM JS ##

### Introduction ###

Working with javascript and HTML usually it is needed to generate HTML DOM estructures. Javascript provides a full set of functions to do this: createElement(), createTextNode(), setAttribute(), ... The problem with these functions is that the code generated is verbose and difficult to read in comparison with the HTML syntax. To help with this "Generate DOM JS" provides the functions to help to create HTML DOM easy to write and to understand.

### How it works ###

There are two ways of creating HTML DOM with "Generate DOM JS". You can use whatever you preffer. Both are equivalents.

You can use the JSON style.

    DOM({
        tag: 'div',
        attr: {
          id: 'mynewdiv'
        },
        children: [
          { tag: 'br' },
          { tag: 'a',
            attr: { href: 'http://www.google.com' },
            children: ['This is a link']
          },
          { tag: 'hr' },
          { tag: 'span',
            attr: { 'class': 'stylingclass' },
            children: ['Lorem ipsum']
          }
        ]
    })

Or the convenient NODE() function.

    DOM(NODE('div', {id: 'mynewdiv'}, [
          NODE('br'),
          NODE('a', { href: 'http://www.google.com' }, ['This is a link']),
          NODE('hr'),
          NODE('span', { 'class': 'stylingclass' }, ['Lorem ipsum'])
    ]))

Both examples create the same HTML DOM:

    <div id="mynewdiv">
      <br/>
      <a href="http://www.openbravo.com">This is a link</a>
      <hr/>
      <span class="stylingclass">Lorem ipsum</spam>
    </div>

In comparison this is the standard way of generating the same HTML DOM using the standard functions:

    var mynewdiv = document.createElement('div');
    mynewdiv.setAttribute('id', 'mynewdiv');
    
    var mybr = document.createElement('br');
    
    var mya = document.createElement('a');
    mya.setAttribute('href', 'http://www.google.com');
    mya.appendChild(document.createTextNode('This is a link'));
    
    var myhr = document.createElement('hr');
    
    var myspan = document.createElement('span');
    myspan.setAttribute('class', 'stylingclass');
    myspan.appendChild(document.createTextNode('Lorem ipsum'));
    
    mynewdiv.appendChild(mybr);
    mynewdiv.appendChild(mya);
    mynewdiv.appendChild(myhr);
    mynewdiv.appendChild(myspan);

### Combining HTML DOM parts ###

If you create diferent parts of HTML DOM and need to combine all parts together, Generate DOM JS can help too. For example:

    var part = DOM(NODE('span', {}, ['Lorem ipsum']));
    
    var container = DOM(NODE('div', {id: 'mynewdiv'}, [
          NODE('hr'),
          part,
          NODE('hr')
    ]))

### Using JQuery ###

The HTML DOM created with "Generate DOM JS" can also interact with JQuery easily.

Including HTML DOM created with Generate DOM JS in a JQuery object

    var newdiv = $(DOM({
        tag : 'div',
        attr: { id : 'mydiv' },
        children: ['Lorem ipsum']
    }));
    
    $('#otherdiv').append(newdiv);

And including a JQuery object in an HTML DOM generated with Generate DOM JS.

    var jquerydiv = $('<div/>').text('This is a JQuery div');
    
    var newdiv = $(DOM({
        tag : 'div',
        attr: { id : 'mydiv' },
        children: [jquerydiv]
    }));




