#HackThis - Real -  Level 3

URL:      https://www.hackthis.co.uk/levels/real/3

##Write Up Iker

Para jugar a este juego es necesario registrarse, así que nos registramos y accedemos a la página para empezar los retos.

##Hint

```html
A friend of yours is getting really annoyed with his school network, they have blocked all the fun stuff. He has found the administrator login page, he's looked through the source code but still doesn't know what to do. Help him out by gaining access to the right account to change the internet settings:

Try and find some more information about the code being used, it will save you a lot of time
```

## Explicación

El enunciado nos indica que estamos en una red donde el administrador ha bloqueado todas pa´ginas divertidas. Un compañero ha conseguido la página de login del administrador pero no sabe que hacer con ella. Nos pide ayuda para que pueda entrar y cambiar la configuración

Entramos a la página web y lo primero que vemos son dos campos:

```html
Member Name:
Password:

Login  Cancel
```

No nos dan más información, por lo que vamosa ver el código de esta página web

```javascript

var m=new Array();
var alpha="abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789abcdefghij";

function box(part,c,r)
{ 
  prms=new Array(r,c); typ=new Array("rowspan=","colspan=");
  bx=new Array("<tr>","</tr>","</tr><tr>","</table>"); 
  clr=new Array("808080","c0c0c0","ffffff","000000");
  img='<img src="blank.gif" width=1 height=1>'; txt="";
  bx[bx.length]='<table border=0 cellpadding=0 cellspacing=0>';
  
  for(bi=0;bi<4;bi++)
  { 
    for(bj=0;bj<2;bj++)
      bx[bx.length]='<td '+typ[bj]+(2*bi+prms[bj]);
      bx[bx.length]=' bgcolor="#'+clr[bi]+'">'+img+'</td>'; 
  };

  ord=new Array();
  
  ord[0]=new Array(4,0,14,16,12,16,14,16,2,11,13,9,13,11,7,2,8,10,6,10,8,10,1);
  ord[1]=new Array(0,6,10,2,9,7,2,12,16,1,3);

  for(bi=0;bi<ord[part].length;bi++)
    txt+=bx[ord[part][bi]]+"\n";
  return txt; 
};

function check(frm)
{ 
  var ary=new Array(0,1,1,7,9,8); 
  f=new Array();
  
  for(i=0;i<3;i++)
    ary[i]=makehash(frm.elements[ary[i]].value,ary[i+3]);
    for(i=0;i<m.length;i++)
      if(m[i][0]==ary[0]) f[f.length]=i;
        if(f.length==0) { alert("Member Not Found"); return; };

   for(i=0;i<f.length;i++)
    if(m[f[i]][1]==ary[1])
     { 
      ary[2]+=" ";
       for(j=2;j<m[f[i]].length;j++)
       { 
        t=""; cnt=0;
          for(k=0;k<m[f[i]][j].length;k++)
          { 
            c=m[f[i]][j].substring(k,k+1);
            a=alpha.indexOf(c,9);
            if(a>-1)
            { 
              b=a-(ary[2].substring(cnt,cnt+1)*1);
              c=alpha.substring(b,b+1);
              cnt=(cnt+1)%(ary[2].length-1); 
            };
            t+=c; 
          };

          m[f[i]][j]=t; 
      };
      window.location=m[f[i]][3];
      return; 
    };
   alert("Incorrect Password!");
 };

function makehash(str,mult)
{ 
  hash=0;
   for (j=0;j<str.length;j++)
    hash=hash*mult+alpha.indexOf(str.substring(j,j+1),0)+1;
    return hash; 
};
```

Menudo chorrazo de código :cry:

Vamos a ir poco a poco entendiendo que es lo que hace el código.
