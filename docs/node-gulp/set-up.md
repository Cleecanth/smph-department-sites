# Node and Gulp Set up

_Note: Most of these instructions are platform agnostic, but some specifics are aimed at Windows users. For the most part, you can swap the words "Windows" and "Command Prompt" with "Mac/Linux" and "Terminal"._

1. Install [Node.js from here](http://www.nodejs.org/).

  * It's recommended to use the 4.x download, since it currently has the best compatibility with the modules we need.

  * Unless you know the implications of (and how the troubleshoot) not using the default options, **run the installer as is**.

2. Install [Git from here](https://git-scm.com/downloads).

  * Under "Adjusting your PATH environment", make sure to select **Use Git from the Windows Command Prompt**.

  * Alternatively, you can install [Github Desktop](https://desktop.github.com/), which will do the same thing and provide you with a pretty nice - if overly simple - GUI.

3. Open Command Prompt (cmd.exe) or Power Shell.

   1. Navigate to the project folder using `cd C:\path\to\project`
   2. Run `npm install gulp -global`
     * You may see an warning about lodash. This is a [known issue](https://github.com/gulpjs/gulp/issues/1485), and nothing to worry about.
   3. Run `npm install`
     * You may see a few warnings and errors. Warnings can usually be ignored. Any errors about Python can also be ignored. We can worry about other errors later.
     * This should take about 1-3 minutes depending on your PC and network connection.

4. From the command prompt, run `gulp serve`
  * You should see something like this:
    ```CLI
    [17:58:14] Using gulpfile ~\smph-department-sites\gulpfile.js
    [17:58:18] Starting '...'...
    -------------------------------------
      Gulp Started
      Ctrl + C to stop
    -------------------------------------
    [17:58:18] Finished '...' after .43 ms
    [17:58:18] Starting 'watch'...
    [17:58:18] Finished 'watch' after .60 ms
    [17:58:18] Starting 'browserSync'...
    [17:58:18] Finished 'browserSync' after 223 ms
    [17:58:18] Starting 'serve'...
    [17:58:18] Finished 'serve' after .18 ms
    [Browser ] Access URLs:
    -------------------------------------
      Local: http://localhost:3000
      External: http://10.1.1.20:3000
    -------------------------------------
      UI: http://localhost:3030
      UI External: http://10.1.1.20:3030
    -------------------------------------
    [Browser ] Serving files from: ./
    [Browser ] Watching files...
    ```

  * Errors about git typically mean you did not install git correctly. Please see step 2 and make sure you select **Use Git from the Windows Command Prompt**. If you are seeing this error after installing Github Desktop, try using the the Git Shell program instead of the command prompt.

  * If you get any other errors, please [file an issue](https://github.com/UWHealth/smph-department-sites/issues) and we'll try to step you through the problem.


5. Open a browser and go to [http://localhost:3000](http://localhost:3000) to see your site up and running.

6. From here, you can edit any files from the `/_partials` folder, where they will compile upon saving. Your browser should refresh the page automatically on save.
