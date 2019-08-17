# HIP for VSCode (syntax + snippets)

This extension aims at providing syntax support and snippets for HIP (C++) in VS Code.

And this project is fork of the vscode-cuda(https://github.com/kriegalex/vscode-cuda) project.

## Features

### Code coloring
This extension supports most of the basic HIP keywords and functions, such as but not limited to :

- hipMalloc, hipFree, ...
- \_\_global\_\_, \_\_device\_\_, \_\_host\_\_, ...
- atomicAdd, atomicSub, surfCubemapLayeredread, ...
- \_\_shfl_down, \_\_syncthreads, ...

![code-coloring](images/code-coloring.gif)

To maximize compatibility with existing popular themes, [textmate language grammar guidelines](https://manual.macromates.com/en/language_grammars#naming_conventions) have not always been respected (external libraries like HIP in support scope). If your theme still doesn't color the HIP code, you can set them with the template rules below (put this into your VSCode user settings in settings.json). This can also be used to override your theme colors, if you want to separate C++ and HIP colors.

```json
"editor.tokenColorCustomizations": {
    "textMateRules": [
        {
            "scope": "support.function.hip-cpp",
            "settings":{
                "foreground": "#56b6c2"
            }
        },
        {
            "scope": "keyword.function.qualifier.hip-cpp",
            "settings":{
                "foreground": "#56b6c2"
            }
        }
    ]
}
```

#### List of scopes

- **"support.function.hip-cpp"** :             atomicAdd, hipMalloc, hipFree, ...
- **"keyword.function.qualifier.hip-cpp"** : \_\_global\_\_, \_\_host\_\_, \_\_device\_\_, ...
- **"storage.modifier.hip-cpp"** : \_\_constant\_\_, \_\_device\_\_, \_\_shared\_\_, ...
- **"support.type.hip-cpp"** : dim3, uint1, ulong1, ...
- **"variable.language.hip-cpp"** : gridDim, blockIdx, blockDim, threadIdx, warpSize
- **"punctuation.section.kernel"** : the kernel brackets <<< >>>
- **"meta.kernel-call.hip-cpp entity.name.function.c"** : the function name before the <<< >>>

### HIP snippets

The following snippets are available :

- **\_\_s** : __syncthreads();
- **cmal** : hipMalloc((void**)&${1:variable}, ${2:bytes});
- **cmalmng** : hipMallocManaged((void**)&${1:variable}, ${2:bytes});	
- **cmem** : hipMemcpy(${1:dest}, ${2:src}, ${3:bytes}, hipMemcpy${4:Host}To${5:Device});
- **cfree** : hipFree(${1:variable});
- **kerneldef** : \_\_global\_\_ void ${1:kernel}(${2}) {\n}
- **kernelcall** : ${1:kernel}<<<${2},${3}>>>(${4});
- **thrusthv** : thrust::host_vector<${1:char}> v$0;
- **thrustdv** : thrust::device_vector<${1:char}> v$0;

![snippets](images/snippets.gif)

## Requirements

- VSCode 1.18+. Slightly older versions should work, very old versions are not guaranteed to work.
- This extension has been tested with the default VSCode skin (dark+) and the popular One Dark Pro theme. 

## Extension Settings

This extension contributes the following settings:

* none
<!-- * `vship.enable`: enable/disable this extension -->

## Known Issues

- No support for Intellisense navigation through code (right click->Go to definition,...). This will be implemented by [another extension](https://github.com/kazulittlefox/vscode-hiptools) dedicated to IntelliSense and debugging.

## Planned features

Below are listed the features that ideally should be available for this extension. IntelliSense and debugging coexist in ~~[another repository](https://github.com/kazulittlefox/vscode-hiptools).~~ There is no guarantees this features will be implemented.

- Icon for files
- HIP syntax colors as parameters of this extension instead of using "editor.tokenColorCustomizations" in settings.json

## Feature requests & issues

Requests should be made here : https://github.com/kazulittlefox/vscode-HIP/issues

 

## Release Notes

See also the [changelog](CHANGELOG.md)

### 0.1.0

Initial release of vscode-HIP extension

### 0.1.1

Better documentation

-----------------------------------------------------------------------------------------------------------
