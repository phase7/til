## clsx

>#### Found this in [stackoverflow](https://stackoverflow.com/a/57557349)

`clsx` is generally used to conditionally apply a given `className`

This syntax means that some class will only be applied if a given condition evaluates to `true`

    const menuStyle = clsx({
        [classes.root] : true, //always apply
        [classes.menuOpen] : open //only when open === true
    })

In this example `[classes.menuOpen]` (which will evaluate to something like `randomclassName123`) will only be applied if `open === true`

---

`clsx` basically performs a `string` interpolation so you don't have to necessarily use it to conditionally apply classes. There are many supported syntax that you can check in the official [docs](https://www.npmjs.com/package/clsx#usage)

Instead of

 

    <div className={`${classes.foo} ${classes.bar} ${classes.baz}`} />

You can use it like

    const { foo, bar, baz } = classes
    const style = clsx(foo, bar, baz)
    
    return <div className={style} />
