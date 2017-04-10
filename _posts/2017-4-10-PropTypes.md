---
layout: post
title: JSX Spread Attribute
---

Today I got a warming from React saying:
```
Warning: Accessing PropTypes via the main React package is deprecated. Use the prop-types package from npm instead.
```
Now PropTypes is extracted from the React package and placed in a separate package named `prop-types`. The following example is from [React blog](https://facebook.github.io/react/blog/2017/04/07/react-v15.5.0.html).
```
import React from 'react';
import PropTypes from 'prop-types';

class Component extends React.Component {
  render() {
    return <div>{this.props.text}</div>;
  }
}

Component.propTypes = {
  text: PropTypes.string.isRequired,
};
```