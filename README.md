Набор утилит для компиляции и генерации доков для react компонентов
===================================================================

componentPackage
----------------

Плагин для создания package.json из всех файлов. Нужен для упрощения импортов. В случае, если ваша библиотека имеет
структуру типа

```
component-name/
    component-name.js
```

создание `package.json` поможет использовать этот компонент как `require('library-name/component-name')`.

Пример использования:

```js
const componentPackage = require('library-tools/component-package');

gulp.src('file.js')
    .pipe(componentPackage())
    .pipe(gulp.dest('dist');
```

В результате в папке `dist` будет создан файл `package.json`:

```json
{ "main": "file.js", "typings": "file.d.ts" }
```


componentTypings
----------------

Плагин для создания `d.ts` файлов на основе react компонентов. Внутри использует библиотеку
[react-to-typescript-definitions](https://www.npmjs.com/package/react-to-typescript-definitions).
Поддерживается генерация только из es6+ кода (не будет работать для уже скомпилированного кода).

Пример использования:

```js
const componentTypings = require('library-tools/component-typings');

gulp.src('file.js')
    .pipe(componentTypings('libraryName'))
    .pipe(gulp.dest('dist');
```

В результате в папке `dist` будет создан файл `file.d.ts`.

```ts
declare module 'libraryName/file' {
    import * as React from 'react';
    export interface FileProps {
        /**
         * Управление видимостью компонента
         */
        visible?: boolean;
    }
    export default class File extends React.Component<LoaderProps, any>{
    }
}
```

Параметры:

- `libraryName` - префикс для названия модулей. В итоговых d.ts файлах имя модуля будет создаять из
`libraryName + '/' + filename`.


componentDocs
-------------

Плагин для создания документации для react компонентов.

Пример использования:

```js
const componentDocs = require('library-tools/component-docs');

gulp.src('file.js')
    .pipe(componentDocs('libraryName'))
    .pipe(gulp.dest('docs');
```

В результате в папке `docs` будет создан файл `README.md`, с описанием props и пубичных методов компонента.

libraryDoc
----------

Плагин для создания индексного файла документации.

Пример использования:

```js
const libraryDoc = require('library-tools/library-doc');

gulp.src('src/*.js')
    .pipe(libraryDoc('libraryName'))
    .pipe(gulp.dest('docs');
```