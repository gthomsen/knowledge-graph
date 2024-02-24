Tags: #utilities 

Tools -> Macro -> Visual Basic Editor.  Create a new module and paste the following code:
```
Sub ChangeFont()
    With ActiveWindow.Selection.TextRange.Font
        .Name = "Courier New"
        .Size = .Size - 2
    End With
End Sub
```

`ChangeFont` is now accessible via Tools -> Macro -> Macros... or from the View ribbon.

Requires saving the presentation in a format that contains macros, which is not `.pptx`.  Attempting to save with the extension `.pptx` will delete the macros.