# 商品线新技术体系基础工具

主要依赖

- `EventEmitter` 依赖于 events@3 https://www.npmjs.com/package/events
- `Queue` 依赖于 queue@6 https://www.npmjs.com/package/queue
- `Middleware` 参考来自：`js-middleware`


简单工具：

- `classNames`: typeof classNames;
- `compose`: (...funcs: Function[]) => Function;
- `executeSafe`: (method: () => any, defaultValue?: any) => any;
- `format`: (tplString: string, dataMap: Record<string, any>) => string;
- `getGuid`: (operator: string | true) => string;
- `getNumberValue`: (value: any, opts?: import("./getNumberValue").GetNumberValueOption) => number;
- `hashCode`: (source: string) => number;
- `isMatches`: (handle: Function | RegExp | any[], params: any) => boolean;
- `observe`: (object: any, keyName: string, callback: (prev: any, next: any) => void) => void;
- `parseParam`: (query: string, options?: XParseOptions) => import("query-string").ParsedQuery<string>;
- `parseUrl`: (url: string, options?: XParseOptions) => import("query-string").ParsedUrl;
- `throwAsync`: (error: string | Error) => void;
- `toParam`: (queryParams: Record<string, any>, options?: import("./parseUrl").XParseOptions) => string;
- `toUrl`: (url: string, queryParams: StringifiableRecord, options?: .XParseOptions) => string;
- `warning`: (...messages: any[]) => void;

浏览器工具：

- `callbackCurrentJsonp`: (result: any) => void;
- `download`: (data: string | Blob, filename: string, gcTimeout: number) => void;
- `getCurrentScript`: typeof getCurrentScript;
- `getEventAnchorId`: (event: Event, defaultValue?: string) => string;
- `getEventAnchorId`: (event: Event, defaultValue?: string) => string;
- `lastSeconds`: () => (stop?: boolean) => number;
- `loadCss`: (url: string, callback?: Function) => void;
- `loadScript`: (url: string, callback?: Function) => void;
- `scrollInView`: (element: HTMLElement, compensation?: any) => void;
