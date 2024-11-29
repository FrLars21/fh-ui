# sidebar


<!-- WARNING: THIS FILE WAS AUTOGENERATED! DO NOT EDIT! -->

``` python
import fasthtml.common as fh
from fh_ui.core import *
```

``` python
def SidebarLayout(*args, **kwargs):
    return fh.Div(fh.Style("me { display: flex; width: 100%; min-height: 100svh; }"), *args, **kwargs)
```

``` python
def Sidebar(*args, **kwargs):
    return fh.Div(id="sidebar-render", data_state="expanded")(
        fh.Style("""
        me { 
            width: 16rem; 
            height: 100svh; 
            position: relative; 
            display: flex; 
            flex-direction: column; 
            border-right: 1px solid var(--zinc-200); 
            background: var(--zinc-100); 
            transition: width 200ms linear;
        }
        me[data-state="collapsed"] { width: 0; }
        me > * { opacity: 1; transition: opacity 100ms linear 100ms; }
        me[data-state="collapsed"] > * { opacity: 0; transition: opacity 100ms linear; }
        me[data-state="collapsed"] #sidebar-rail { cursor: e-resize; }
        """),
        *args, **kwargs)
```

``` python
def SidebarHeader(*args, **kwargs):
    return fh.Div(fh.Style("me { display: flex; flex-direction: column; gap: 0.5rem; padding: 0.5rem }"), *args, **kwargs)
```

``` python
def SidebarFooter(*args, **kwargs):
    return fh.Div(fh.Style("me { display: flex; flex-direction: column; gap: 0.5rem; padding: 0.5rem }"), *args, **kwargs)
```

``` python
def SidebarContent(*args, **kwargs):
    return fh.Div(
        fh.Style("""
        me { display: flex; min-height: 0px; flex: 1 1 0%; flex-direction: column; gap: 0.5rem; overflow: auto; }
        """), *args, **kwargs)
```

``` python
def SidebarRail():
    return fh.Button(
        fh.Style("""
        me {
            cursor: w-resize;
            position: absolute;
            right: -1rem;
            top: 0;
            bottom: 0;,
            z-index: 20;
            width: 1rem;
            transform: translateX(-50%);
            transition: all linear;
            /* display: none; */
            display: flex;
            background: transparent;
            border-width: 0;
        }
        
        me::after {
            content: '';
            position: absolute;
            top: 0;
            bottom: 0;
            width: 2px;
        }
        
        me:hover::after { background-color: var(--zinc-300); }
    
        """), 
        id="sidebar-rail",
        hx_on_click="htmx.find('#sidebar-render').dataset.state = htmx.find('#sidebar-render').dataset.state === 'collapsed' ? 'expanded' : 'collapsed'",
        aria_label="Toggle Sidebar", tabindex="-1", title="Toggle Sidebar")
```

``` python
def MainContent(*args, **kwargs):
    return fh.Div(fh.Style("me { min-height: 100svh; }"), *args, **kwargs)
```

## Demo

``` python
hdrs
```

    [link((),{'rel': 'preconnect', 'href': 'https://rsms.me/'}),
     link((),{'rel': 'stylesheet', 'href': 'https://rsms.me/inter/inter.css'}),
     script(('',),{'src': 'https://unpkg.com/htmx.org@next/dist/htmx.min.js'}),
     script(('',),{'src': 'https://cdn.jsdelivr.net/gh/answerdotai/fasthtml-js@1.0.4/fasthtml.js'}),
     script(('',),{'src': 'https://cdn.jsdelivr.net/gh/answerdotai/surreal@main/surreal.js'}),
     script(('',),{'src': 'https://cdn.jsdelivr.net/gh/gnat/css-scope-inline@main/script.js'}),
     style(("\n    :root {\n      --zinc-50: #fafafa;\n      --zinc-100: #f4f4f5;\n      --zinc-200: #e4e4e7;\n      --zinc-300: #d4d4d8;\n      --zinc-400: #a1a1aa;\n      --zinc-500: #71717a;\n      --zinc-600: #52525b;\n      --zinc-700: #3f3f46;\n      --zinc-800: #27272a;\n      --zinc-900: #18181b;\n      --zinc-950: #09090b;\n\n      --red-50: #fef2f2;\n      --red-100: #fee2e2;\n      --red-200: #fecaca;\n      --red-300: #fca5a5;\n      --red-400: #f87171;\n      --red-500: #ef4444;\n      --red-600: #dc2626;\n      --red-700: #b91c1c;\n      --red-800: #991b1b;\n      --red-900: #7f1d1d;\n      --red-950: #450a0a;  \n\n      font-size: 1rem;\n      font-family: Inter, sans-serif;\n      font-feature-settings: 'liga' 1, 'calt' 1; /* fix for Chrome */\n    }\n    @supports (font-variation-settings: normal) {\n        :root { font-family: InterVariable, sans-serif; }\n    }\n    ",),{})]

``` python
fh.show(*hdrs,
    SidebarLayout(
        Sidebar(
            SidebarHeader(
                fh.Style("me { border-bottom: 1px solid var(--zinc-200); }"),
                Button(fh.Style("me { anchor-name: --myAnchor; }"), "open", popover_anchor=True, popovertarget="hdr-popper", variant="outline"),
                fh.Div(id="hdr-popper", popover=True)(
                    fh.Style("me { position: absolute; position-anchor: --myAnchor; top: anchor(bottom); left: anchor(right); }"),
                    fh.P("hdr popper")
                )
            ),
            SidebarContent(fh.Ul(*[fh.Li("Content here") for _ in range(0,50)])),
            SidebarFooter(
                fh.Style("me { border-top: 1px solid var(--zinc-200); }"),
                Button("Footer here")
            ),
            SidebarRail()
        ),
        MainContent(
            fh.Style("me { flex: 1 1 0%; }"),
            fh.Header(
                fh.Style("me { display: flex; padding: 1rem; gap: 1rem; border-bottom: 1px solid var(--zinc-200); }"),
                Button(fh.NotStr("&#9776;"), variant="ghost", hx_on_click="""
            htmx.find('#sidebar-render').dataset.state = htmx.find('#sidebar-render').dataset.state === 'collapsed' ? 'expanded' : 'collapsed'
            console.log(htmx.find('#sidebar-render').dataset.state)
            """),
                fh.Div(fh.Style("me { width: 1px; height: 100%; background: var(--zinc-300); }")),
                fh.Ol(aria_label="breadcrumb")(
                    fh.Style("""
                    me {
                        list-style: none!important;
                        padding: 0px!important;
                        margin: 0px!important;
                        display: flex;
                        flex-wrap: wrap;
                        align-items: center;
                        gap: 0.375rem; /* 1.5 * 0.25rem */
                        word-wrap: break-word;
                        font-size: 0.875rem; /* 14px */
                        color: var(--zinc-600);
                    }
                    """),
                    fh.Li("Home"), fh.Li("Specific")
                )
            ),
            fh.Div(
                fh.Style("""
                me {
                    display: flex;
                    flex-direction: column;
                    gap: 1rem;
                    padding: 1rem;
                    flex: 1 1 0%;
                }
                """),
                fh.Div(
                    fh.Style("""
                    me {
                        display: grid;
                        grid-auto-rows: min-content;
                        gap: 1rem;
                        grid-template-columns: repeat(3, 1fr);
                    }
                    """),
                    *[fh.Div(fh.Style("me { background-color: var(--zinc-50); width: 100%; min-height: 10rem; border-radius: 0.75rem; }"))] * 3
                ),
                fh.Div(fh.Style("me { background-color: var(--zinc-50); width: 100%; min-height: 20rem; border-radius: 0.75rem; }"))
            )
        )
    )
)
```

<link rel="preconnect" href="https://rsms.me/">
<link rel="stylesheet" href="https://rsms.me/inter/inter.css">
<script src="https://unpkg.com/htmx.org@next/dist/htmx.min.js"></script><script src="https://cdn.jsdelivr.net/gh/answerdotai/fasthtml-js@1.0.4/fasthtml.js"></script><script src="https://cdn.jsdelivr.net/gh/answerdotai/surreal@main/surreal.js"></script><script src="https://cdn.jsdelivr.net/gh/gnat/css-scope-inline@main/script.js"></script><style>
    :root {
      --zinc-50: #fafafa;
      --zinc-100: #f4f4f5;
      --zinc-200: #e4e4e7;
      --zinc-300: #d4d4d8;
      --zinc-400: #a1a1aa;
      --zinc-500: #71717a;
      --zinc-600: #52525b;
      --zinc-700: #3f3f46;
      --zinc-800: #27272a;
      --zinc-900: #18181b;
      --zinc-950: #09090b;
&#10;      --red-50: #fef2f2;
      --red-100: #fee2e2;
      --red-200: #fecaca;
      --red-300: #fca5a5;
      --red-400: #f87171;
      --red-500: #ef4444;
      --red-600: #dc2626;
      --red-700: #b91c1c;
      --red-800: #991b1b;
      --red-900: #7f1d1d;
      --red-950: #450a0a;  
&#10;      font-size: 1rem;
      font-family: Inter, sans-serif;
      font-feature-settings: 'liga' 1, 'calt' 1; /* fix for Chrome */
    }
    @supports (font-variation-settings: normal) {
        :root { font-family: InterVariable, sans-serif; }
    }
    </style>
<div>
  <style>me { display: flex; width: 100%; min-height: 100svh; }</style>
  <div data-state="expanded" id="sidebar-render">
    <style>
        me { 
            width: 16rem; 
            height: 100svh; 
            position: relative; 
            display: flex; 
            flex-direction: column; 
            border-right: 1px solid var(--zinc-200); 
            background: var(--zinc-100); 
            transition: width 200ms linear;
        }
        me[data-state="collapsed"] { width: 0; }
        me > * { opacity: 1; transition: opacity 100ms linear 100ms; }
        me[data-state="collapsed"] > * { opacity: 0; transition: opacity 100ms linear; }
        me[data-state="collapsed"] #sidebar-rail { cursor: e-resize; }
        </style>
    <div>
      <style>me { display: flex; flex-direction: column; gap: 0.5rem; padding: 0.5rem }</style>
      <style>me { border-bottom: 1px solid var(--zinc-200); }</style>
<button popover-anchor popovertarget="hdr-popper">        <style>
    me {
        position: relative;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        font-weight: 500;
        gap: 0.5rem;
        white-space: nowrap;
        height: 2.5rem;
        font-size: 0.875rem;
        line-height: 1.25rem;
        border-radius: 0.5rem;
        padding-left: 1rem;
        padding-right: 1rem;
        box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
        cursor: pointer;
        border-style: solid;
        border-width: 0px;
        background-color: transparent;
    }
    me { background-color: white; color: var(--zinc-700); border-width: 1px; border-color: var(--zinc-200); }me:hover { background-color: var(--zinc-50); }</style>
        <style>me { anchor-name: --myAnchor; }</style>
open</button>      <div popover id="hdr-popper">
        <style>me { position: absolute; position-anchor: --myAnchor; top: anchor(bottom); left: anchor(right); }</style>
        <p>hdr popper</p>
      </div>
    </div>
    <div>
      <style>
        me { display: flex; min-height: 0px; flex: 1 1 0%; flex-direction: column; gap: 0.5rem; overflow: auto; }
        </style>
      <ul>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
        <li>Content here</li>
      </ul>
    </div>
    <div>
      <style>me { display: flex; flex-direction: column; gap: 0.5rem; padding: 0.5rem }</style>
      <style>me { border-top: 1px solid var(--zinc-200); }</style>
<button>        <style>
    me {
        position: relative;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        font-weight: 500;
        gap: 0.5rem;
        white-space: nowrap;
        height: 2.5rem;
        font-size: 0.875rem;
        line-height: 1.25rem;
        border-radius: 0.5rem;
        padding-left: 1rem;
        padding-right: 1rem;
        box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
        cursor: pointer;
        border-style: solid;
        border-width: 0px;
        background-color: transparent;
    }
    me { background-color: var(--zinc-800); color: white; border-color: var(--zinc-200); }me:hover { background-color: var(--zinc-900); }</style>
Footer here</button>    </div>
<button hx-on-click="htmx.find('#sidebar-render').dataset.state = htmx.find('#sidebar-render').dataset.state === 'collapsed' ? 'expanded' : 'collapsed'" aria-label="Toggle Sidebar" tabindex="-1" id="sidebar-rail" title="Toggle Sidebar" name="sidebar-rail">      <style>
        me {
            cursor: w-resize;
            position: absolute;
            right: -1rem;
            top: 0;
            bottom: 0;,
            z-index: 20;
            width: 1rem;
            transform: translateX(-50%);
            transition: all linear;
            /* display: none; */
            display: flex;
            background: transparent;
            border-width: 0;
        }
        &#10;        me::after {
            content: '';
            position: absolute;
            top: 0;
            bottom: 0;
            width: 2px;
        }
        &#10;        me:hover::after { background-color: var(--zinc-300); }
    &#10;        </style>
</button>  </div>
  <div>
    <style>me { min-height: 100svh; }</style>
    <style>me { flex: 1 1 0%; }</style>
    <header>
      <style>me { display: flex; padding: 1rem; gap: 1rem; border-bottom: 1px solid var(--zinc-200); }</style>
<button hx-on-click="
            htmx.find('#sidebar-render').dataset.state = htmx.find('#sidebar-render').dataset.state === 'collapsed' ? 'expanded' : 'collapsed'
            console.log(htmx.find('#sidebar-render').dataset.state)
            ">        <style>
    me {
        position: relative;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        font-weight: 500;
        gap: 0.5rem;
        white-space: nowrap;
        height: 2.5rem;
        font-size: 0.875rem;
        line-height: 1.25rem;
        border-radius: 0.5rem;
        padding-left: 1rem;
        padding-right: 1rem;
        box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
        cursor: pointer;
        border-style: solid;
        border-width: 0px;
        background-color: transparent;
    }
    me { box-shadow: none; }me:hover { background-color: var(--zinc-100); }</style>
&#9776;</button>      <div>
        <style>me { width: 1px; height: 100%; background: var(--zinc-300); }</style>
      </div>
      <ol aria-label="breadcrumb">
        <style>
                    me {
                        list-style: none!important;
                        padding: 0px!important;
                        margin: 0px!important;
                        display: flex;
                        flex-wrap: wrap;
                        align-items: center;
                        gap: 0.375rem; /* 1.5 * 0.25rem */
                        word-wrap: break-word;
                        font-size: 0.875rem; /* 14px */
                        color: var(--zinc-600);
                    }
                    </style>
        <li>Home</li>
        <li>Specific</li>
      </ol>
    </header>
    <div>
      <style>
                me {
                    display: flex;
                    flex-direction: column;
                    gap: 1rem;
                    padding: 1rem;
                    flex: 1 1 0%;
                }
                </style>
      <div>
        <style>
                    me {
                        display: grid;
                        grid-auto-rows: min-content;
                        gap: 1rem;
                        grid-template-columns: repeat(3, 1fr);
                    }
                    </style>
        <div>
          <style>me { background-color: var(--zinc-50); width: 100%; min-height: 10rem; border-radius: 0.75rem; }</style>
        </div>
        <div>
          <style>me { background-color: var(--zinc-50); width: 100%; min-height: 10rem; border-radius: 0.75rem; }</style>
        </div>
        <div>
          <style>me { background-color: var(--zinc-50); width: 100%; min-height: 10rem; border-radius: 0.75rem; }</style>
        </div>
      </div>
      <div>
        <style>me { background-color: var(--zinc-50); width: 100%; min-height: 20rem; border-radius: 0.75rem; }</style>
      </div>
    </div>
  </div>
</div>