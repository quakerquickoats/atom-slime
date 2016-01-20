# atom-slime package

Integrates SLIME (the Superior Lisp Interaction Mode for Emacs) with Atom! This package allows you to interactively develop Common Lisp code, helping turn Atom into a full-featured Lisp IDE.

Current features of this package:

- Read-eval-print-loop (REPL) for interactive Lisp development
- Integrated debugger (work in progress on stack trace)
- Jumping to a method definition
- Autocomplete suggestions based on your code
- Function method argument order documentation

Future features:
- Interactive object inspection
- Stack trace in debugger
- "Compile this function" command
- "Who calls this function" command


**Note**: This package is still in beta and in active development! Contributions and bug reports are welcome.



Guide to setting up Atom as your main Lisp editor!
-------------------------------------------
By following this instructions, you can use Atom very effectively as your Lisp editor.

1. Install this `atom-slime` package, as well as `language-lisp` package (syntax highlighting) and the `lisp-paredit` package (proper idiomatic lisp indentation and parenthesis editing)

2. Install a lisp if you don't already have one (such as SBCL)

3. Download the `slime` code, which exists in a separate repository. Place it somewhere safe (you'll need it's location in the following step). Note that if you've used Emacs before, you may already have slime somewhere on your computer. Otherwise, you can download it here:
https://github.com/slime/slime.git

4. After installing the `atom-slime` package, go to its package preferences page within Atom. Under the "Lisp Process" field, enter the executable for your lisp (ex. `sbcl`. Note that on some platforms you may need the full pathname, such as `/usr/bin/sbcl`). Under the "Slime Path" field, enter the path where you have slime on your computer from the above step.

5. (Optional) Consider adding the following to your Atom keymap file:
```
'atom-text-editor[data-grammar~="lisp"]':
    'tab': 'lisp-paredit:indent'
```
This will allow the tab key to trigger automatic, correct indentation of your Lisp code.

All done!


How to Edit Lisp code with Atom
----------------------------
Once you've followed the above steps, you should have:
- Syntax highlighting if you open a file ending in `.lisp`
- Proper lisp indentation when you hit tab

To start a REPL (an interactive terminal where you can interact with Lisp live), run the `Slime: Start` command from the command pallet. A REPL should then pop up. Note that if this is your first time using `atom-slime`, or you've updated your lisp process, you may get some warning messages about not being to connect. Try again in a minute or so and it should work after your lisp has finished compiling the swank code.

With the REPL, you can type commands, see results, switch packages, and more. It's a great way to write Lisp code! A debugger will come up if an error occurs.

If you've compiled your lisp code, placing the cursor over a method will cause a documentation string to appear at the bottom of the atom window, showing you the function arguments and their order.

If you want to jump to where a certain method is defined, go to it and press <kbd>alt</kbd> + <kbd>.</kbd> or use the `Slime: Goto Definition` function in Atom. A little pop up window will come up and ask you which method you'd like to go to (since methods could be overloaded). Use the keyboard to go up and down, and press enter to jump to the definition you choose.



How it works
--------------
This package makes use of the superb work from the slime project. Slime started as a way to integrate Lisp with Emacs, a popular text editor for Lisp. It works by starting what is known as a swank server, which is code that runs in Lisp. Emacs then runs separately and connects to the swank server. It's able to make remote procedure calls to the swank server to compile functions, lookup function definitions from your live code, and much more thanks to the fact that Lisp is such a dynamic language.

This package uses the swank server from the slime project unchanged. This package allows Atom to speak the same protocol as Emacs for controlling the swank server and integrating Lisp into the editor.
