# tobii-pro-sdk-opensesame-example
Example of capturing eyetracker output in OpenSesame using the Tobii Pro SDK

This example uses inline code in OpenSesame to capture eyetracker output, using the Tobii Pro SDK:

http://developer.tobiipro.com/python/python-sdk-reference-guide.html

**You may not need this for your experiment if support for the Tobii Pro SDK has been added to PyGaze and OpenSesame, check first!**

If you want to write any output variables alongside eyetracker data, add them to the list `cols_results` in the inline code item `set_up_eyetracker_output`.

This experiment tries to capture loop variables in OpenSesame and write them alongside eyetracking data. At present this conflicts with a lock in OpenSesame. So do **one** of the following:

1. If you want to capture loop variables alongside eyetracker output, find these lines in var_store.py in your copy of OpenSesame:

```python
    raise osexception(
    u"Recursion detected! Is variable '%s' defined in terms of itself (e.g., 'var = [var]') in item '%s'" \
                                % (var, self.name))
```

Change `raise osexception(` to `warnings.warn(` to disable this error.

2. If you don't want to capture loop variables alongside eyetracker output, go to the inline code item `start_eyetracker` and comment out the code:

```python
    for k in cols_from_loop:
        if var.has(k):
            data[k] = var.get(k)
```
