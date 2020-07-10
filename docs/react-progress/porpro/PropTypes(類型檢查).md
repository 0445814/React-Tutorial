# PropTypes(類型檢查)

類型檢查通常是必須的，它能讓你快速地檢測和捕獲應用的bug。

### prop-types

[prop-types](https://github.com/facebook/prop-types) 是react提供的一個用於類型檢查的包，它可以檢測react組件`props`屬性的合法性。

### prop-types基本使用

##### 1，在組件外部使用

```js
import PropTypes from 'prop-types';

class APP extends React.Component {
  render() {
    return (
      <h1>Hello, { this.props.name }</h1>
    );
  }
}

APP.propTypes = {
    name: PropTypes.string
};  
```

##### 2，在組件內部使用
在組件內部使用時，需要把PropTypes定義為靜態屬性。
```js
import PropTypes from 'prop-types';

class APP extends React.Component {  

  static PropTypes = {
      name: PropTypes.string
  }  

  render() {
    return (
      <h1>Hello, { this.props.name }</h1>
    );
  }
}
```

### prop-types驗證器  

```js
import PropTypes from 'prop-types';

MyComponent.propTypes = {
  // 你可以聲明一個 prop 是一個特定的 JS 原始類型。 
  // 默認情況下，這些都是可選的。
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,
  optionalFunc: PropTypes.func,
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string,
  optionalSymbol: PropTypes.symbol,

  // 任何東西都可以被渲染:numbers, strings, elements,或者是包含這些類型的數組(或者是片段)。
  optionalNode: PropTypes.node,

  // 一個 React 元素。
  optionalElement: PropTypes.element,

  // 你也可以聲明一個 prop 是類的一個實例。 
  // 使用 JS 的 instanceof 運算符。
  optionalMessage: PropTypes.instanceOf(Message),

  // 你可以聲明 prop 是特定的值，類似於枚舉
  optionalEnum: PropTypes.oneOf(['News', 'Photos']),

  // 一個對象可以是多種類型其中之一
  optionalUnion: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Message)
  ]),

  // 一個某種類型的數組
  optionalArrayOf: PropTypes.arrayOf(PropTypes.number),

  // 屬性值為某種類型的對象
  optionalObjectOf: PropTypes.objectOf(PropTypes.number),

  // 一個特定形式的對象
  optionalObjectWithShape: PropTypes.shape({
    color: PropTypes.string,
    fontSize: PropTypes.number
  }),

  // 你可以使用 `isRequired' 連結上述任何一個，以確保在沒有提供 prop 的情況下顯示警告。
  requiredFunc: PropTypes.func.isRequired,

  // 任何數據類型的值
  requiredAny: PropTypes.any.isRequired,

  // 你也可以聲明自訂的驗證器。如果驗證失敗返回 Error 對象。不要使用 `console.warn` 或者 throw ，
  // 因為這不會在 `oneOfType` 類型的驗證器中起作用。
  customProp: function(props, propName, componentName) {
    if (!/matchme/.test(props[propName])) {
      return new Error(
        'Invalid prop `' + propName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  },

  // 也可以聲明`arrayOf`和`objectOf`類型的驗證器，如果驗證失敗需要返回Error對象。
  // 會在數組或者對象的每一個元素上調用驗證器。驗證器的前兩個參數分別是數組或者對象本身，
  // 以及當前元素的鍵值。
  customArrayProp: PropTypes.arrayOf(function(propValue, key, componentName, location, propFullName) {
    if (!/matchme/.test(propValue[key])) {
      return new Error(
        'Invalid prop `' + propFullName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  })
};
```