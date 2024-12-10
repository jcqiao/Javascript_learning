## 1.What is your experience using webpack

Webpack is a powerful module bundler that allows us to bundle multiple JavaScript files into a single file, which is necessary for browsers to efficiently load applications. Without Webpack, you would need to include a **script** tag for every JavaScript file, which becomes impractical in larger applications with hundreds of files. Webpack simplifies this by parsing all files, analyzing dependencies based on import and export statements, and bundling them together into one or more optimized bundles.

In addition to bundling, Webpack enables various optimizations, such as code splitting, tree shaking, and minification, which improve performance. I have some experience working with Webpack, including setting up projects from scratch and configuring loaders and plugins to handle tasks like compiling TypeScript, processing CSS or LESS, and optimizing production builds. I'm also familiar with using plugins like HtmlWebpackPlugin for automating HTML generation and TerserPlugin for minifying JavaScript.

## 2.Since you’ve worked a lot with Webpack and configured projects from scratch, can you walk me through how you would set up a basic Webpack configuration for a React application? Specifically, how would you handle Babel for JSX transpilation and CSS file processing?

To set up a basic webpack configuration, I would start by initializing the project using ==npm init== to create ==package.json==. Then I'd install the necessary dependencies, including webpack, webpack-cli, react, Babel and loaders for transpilation and CSS processing.For example, I’d install Babel with presets like @babel/preset-env and @babel/preset-react for handling modern JavaScript and JSX.

Next, I’d create a webpack.config.js file. The entry point would be the main JavaScript file, like src/index.js, and the output would specify the bundled file, typically in a dist directory. For handling React, I’d set up Babel with a babel-loader rule to transpile JavaScript and JSX files, excluding node_modules. For styles, I’d configure CSS processing with style-loader and css-loader.

Then add scripts into package.json, like start: webpack serve. build: webpack

```javascript
module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js",
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: "babel-loader",
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
      },
    ],
  },
  resolve: {
    extensions: [".js", ".jsx"],
  },
  devServer: {
    static: "./dist", // Serve files from the dist directory
    hot: true, // Enable hot module replacement
  },
  mode: "development",
};
```

## 3.Are you familiar with tree shaking

Yes, It’s basically what happens at build time to optimize the bundle. Webpack analyzes the code to find any modules or parts of modules that were imported but aren’t actually being used in the application. Then it removes them to keep the bundle as small as possible.

This process helps improve web performance because a smaller bundle means faster load times and less memory usage for the browser. It’s a great way to ensure the application is efficient and performs well for users.

## 4. Have you use tree shaking professionally in production at any stage, can you give me an example

Yes, I have used tree shaking professionally in production, especially when optimizing bundle sizes. As of Webpack 5, tree shaking is enabled by default when the mode is set to production. This means that Webpack automatically analyzes the dependency graph and removes unused code from the final bundle.

One key aspect of tree shaking is that it works effectively with ES6 static imports (import/export), as these allow Webpack to determine the exact usage of modules at build time. For example, if you have a utility library but only use a few functions, Webpack will exclude the unused functions from the final bundle.

However, there are limitations. Tree shaking doesn't work for CommonJS and dynamic imports, because they are determined at running time. So if the libraries or dependencies are not tree-shaking-friendly (e.g., they don’t use ES6 modules), unused parts of the code will still be bundled.

In my case, I encountered a scenario where a third-party library was increasing the bundle size significantly. Upon inspection, I realized it wasn’t tree-shaking-friendly because it used CommonJS. To resolve this, I find alternative libary that supported ES6 modules. This reduced the bundle size and improved load times for the application.
