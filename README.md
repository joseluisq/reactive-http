# Reactive HTTP ![devel](https://github.com/joseluisq/reactive-http/workflows/devel/badge.svg?branch=master) [![npm](https://img.shields.io/npm/v/reactive-http.svg)](https://www.npmjs.com/package/reactive-http) [![npm](https://img.shields.io/npm/dt/reactive-http.svg)](https://www.npmjs.com/package/reactive-http) [![docs](https://img.shields.io/badge/docs-latest-green)](https://joseluisq.github.io/reactive-http/)

> HTTP [`Fetch` API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) client over [RxJS `Observables`](https://rxjs.dev/guide/overview) inspired by [Angular `HttpClient`](https://angular.io/api/common/http/HttpClient).

## Install

```sh
npm install rxjs@^7 reactive-http --save
# or
yarn add rxjs@^7 reactive-http
```

## Usage

```ts
// import { catchError, of } from 'rxjs'
import { Observable } from 'rxjs'
import { Http, HttpHandler, HttpInterceptor } from 'reactive-http'

class Interceptor1 implements HttpInterceptor {
    intercept(req: Request, next: HttpHandler): Observable<Response> {
        console.log("first interceptor!")
        return next(req)
    }
}

class Interceptor2 implements HttpInterceptor {
    intercept(req: Request, next: HttpHandler): Observable<Response> {
        console.log("second interceptor!")
        return next(req)
    }
}

interface Repository {
    id: number,
    name: string,
    description: string,
    html_url: string,
}

const http = new Http()
http.intercept(new Interceptor1())
http.intercept(new Interceptor2())

const ob$ = http.get<Repository>('https://api.github.com/repos/joseluisq/reactive-http')
// .pipe(
//     catchError(err => {
//         console.error(err)
//         return of({ error: false, message: err.message })
//     })
// )

ob$.subscribe(resp => {
    console.log('id:', resp.id)
    console.log('name:', resp.name)
    console.log('description:', resp.description)
})
```

## API

See [reactive-http documentation](https://joseluisq.github.io/reactive-http/) page.

## Contributions

Feel free to send a [Pull request](https://github.com/joseluisq/reactive-http/pulls) or file an [issue](https://github.com/joseluisq/reactive-http/issues).

## License
MIT license

© 2023-present [Jose Quintana](https://github.com/joseluisq)
