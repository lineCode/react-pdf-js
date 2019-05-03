# react-pdf-js

`react-pdf-js` provides a component for rendering PDF documents using [PDF.js](http://mozilla.github.io/pdf.js/).

---
[![NPM Version](https://img.shields.io/npm/v/react-pdf-js.svg?style=flat-square)](https://www.npmjs.com/package/react-pdf-js)
[![NPM Downloads](https://img.shields.io/npm/dm/react-pdf-js.svg?style=flat-square)](https://www.npmjs.com/package/react-pdf-js)
[![Build Status](https://travis-ci.com/mikecousins/react-pdf-js.svg?branch=master)](https://travis-ci.com/mikecousins/react-pdf-js)
[![Dependency Status](https://david-dm.org/mikecousins/react-pdf-js.svg)](https://david-dm.org/mikecousins/react-pdf-js)
[![devDependency Status](https://david-dm.org/mikecousins/react-pdf-js/dev-status.svg)](https://david-dm.org/mikecousins/react-pdf-js#info=devDependencies)
[![Netlify Status](https://api.netlify.com/api/v1/badges/4ce8e5b5-16ca-4942-8c47-095debbc4693/deploy-status)](https://app.netlify.com/sites/pdf/deploys)

## Demo

https://pdf.netlify.com

## Usage

Install with `yarn add react-pdf-js` or `npm install react-pdf-js`

Use it in your app (showing some basic pagination as well):

```js
import React from 'react';
import PDF from 'react-pdf-js';

class MyPdfViewer extends React.Component {
  state = {};

  onDocumentComplete = (pages) => {
    this.setState({ page: 1, pages });
  }

  handlePrevious = () => {
    this.setState({ page: this.state.page - 1 });
  }

  handleNext = () => {
    this.setState({ page: this.state.page + 1 });
  }

  renderPagination = (page, pages) => {
    let previousButton = <li className="previous" onClick={this.handlePrevious}><a href="#"><i className="fa fa-arrow-left"></i> Previous</a></li>;
    if (page === 1) {
      previousButton = <li className="previous disabled"><a href="#"><i className="fa fa-arrow-left"></i> Previous</a></li>;
    }
    let nextButton = <li className="next" onClick={this.handleNext}><a href="#">Next <i className="fa fa-arrow-right"></i></a></li>;
    if (page === pages) {
      nextButton = <li className="next disabled"><a href="#">Next <i className="fa fa-arrow-right"></i></a></li>;
    }
    return (
      <nav>
        <ul className="pager">
          {previousButton}
          {nextButton}
        </ul>
      </nav>
    );
  }

  render() {
    let pagination = null;
    if (this.state.pages) {
      pagination = this.renderPagination(this.state.page, this.state.pages);
    }
    return (
      <div>
        <PDF
          file="test.pdf"
          onDocumentComplete={this.onDocumentComplete}
          page={this.state.page}
        />
        {pagination}
      </div>
    );
  }
}

export default MyPdfViewer;
```

## Known Issues

When using Create React App 3.0 you'll get some warnings about:
> ./node_modules/pdfjs-dist/build/pdf.js
Critical dependency: require function is used in a way in which dependencies cannot be statically extracted

Issues have been logged with create-react-app and pdf.js about this issue.

## License

MIT © [mikecousins](https://github.com/mikecousins)
