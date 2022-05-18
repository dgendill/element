# How To Build on Windows

1. Run yarn in project root

2. Run `npm run clean; npm run build:file; npm run lint; npm run webpack -- --config build/webpack.conf.js; npm run webpack -- --config build/webpack.common.js; npm run webpack -- --config build/webpack.component.js; npm run build:utils; npm run build:umd; npm run build:theme`

# Support Object Keys with Special Characters Proposal

1. Support non-word characters in prop and ref keys.
2. Fixes "Error: please transfer a valid prop path to form item!" when an object key contains non-word characters like period or semicolon.

For Example, if you had an object structured like this...

```
{
  ratings: {
    "Mt. Fiji": 1,
    "Mountain: Mt. Blanca": 2,
  }
}
```

If you tried to validate those fields with a ref or a prop you would get the "Error: please transfer a valid prop path to form item!" error because
the semicolon and period would be stripped in the getPropByPath function.

```
<el-form :model="form" :rules="rules" ref="form">
  <el-form-item
    :prop="`ratings.${mountain}`"
    :rules="{ type: 'string', trigger: 'blur', required: true, message: 'A rating is required.'}"
    >
    <el-input
      :ref="`form.ratings.${mountain}`"
      v-model="form.rating[mountain]" maxlength="3">
    </el-input>
  </el-form-item>
</el-form>
```

Updating the regexp in the getPropByPath function is my proposal but it requires negative lookbehind. There may be a way to
remove the negative lookbehind requirement: https://stackoverflow.com/a/7376612/15928632

---

1. Move to support ES2018 so we can use negative lookbehind in regexp:
https://github.com/eslint/eslint/issues/11564#issuecomment-478132319

2. It may be rare, but others have run needed upport for non-word characters like a period or a semicolon in the object keys used in props and refs.
https://github.com/ElemeFE/element/issues/10293
https://github.com/ElemeFE/element/issues/17893


3. form-item.vue contains this check. Is this necessary or an unneeded artifact that can be removed.

```
if (path.indexOf(':') !== -1) {
path = path.replace(/:/, '.');
}```

      
      
      non-word 
      