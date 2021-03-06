<div itemscope itemtype="http://developers.google.com/ReferenceObject">
<meta itemprop="name" content="tf_agents.environments.py_environment.PyEnvironment" />
<meta itemprop="path" content="Stable" />
<meta itemprop="property" content="batch_size"/>
<meta itemprop="property" content="batched"/>
<meta itemprop="property" content="__enter__"/>
<meta itemprop="property" content="__exit__"/>
<meta itemprop="property" content="__init__"/>
<meta itemprop="property" content="action_spec"/>
<meta itemprop="property" content="close"/>
<meta itemprop="property" content="current_time_step"/>
<meta itemprop="property" content="observation_spec"/>
<meta itemprop="property" content="render"/>
<meta itemprop="property" content="reset"/>
<meta itemprop="property" content="seed"/>
<meta itemprop="property" content="step"/>
<meta itemprop="property" content="time_step_spec"/>
</div>

# tf_agents.environments.py_environment.PyEnvironment

<table class="tfo-notebook-buttons tfo-api" align="left">
</table>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

## Class `PyEnvironment`

Abstract base class for Python RL environments.



<!-- Placeholder for "Used in" -->

Observations and valid actions are described with `ArraySpec`s, defined in
the `specs` module.

If the environment can run multiple steps at the same time and take a batched
set of actions and return a batched set of observations, it should overwrite
the property batched to True.

<h2 id="__init__"><code>__init__</code></h2>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
__init__()
```

## Properties

<h3 id="batch_size"><code>batch_size</code></h3>

The batch size of the environment.

#### Returns:

The batch size of the environment, or `None` if the environment is not
batched.

#### Raises:

*   <b>`RuntimeError`</b>: If a subclass overrode batched to return True but did
    not override the batch_size property.

<h3 id="batched"><code>batched</code></h3>

Whether the environment is batched or not.

If the environment supports batched observations and actions, then overwrite
this property to True.

A batched environment takes in a batched set of actions and returns a
batched set of observations. This means for all numpy arrays in the input
and output nested structures, the first dimension is the batch size.

When batched, the left-most dimension is not part of the action_spec
or the observation_spec and corresponds to the batch dimension.

#### Returns:

A boolean indicating whether the environment is batched or not.

## Methods

<h3 id="__enter__"><code>__enter__</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
__enter__()
```

Allows the environment to be used in a with-statement context.

<h3 id="__exit__"><code>__exit__</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
__exit__(
    unused_exception_type,
    unused_exc_value,
    unused_traceback
)
```

Allows the environment to be used in a with-statement context.

<h3 id="action_spec"><code>action_spec</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
action_spec()
```

Defines the actions that should be provided to `step()`.

May use a subclass of `ArraySpec` that specifies additional properties such
as min and max bounds on the values.

#### Returns:

An `ArraySpec`, or a nested dict, list or tuple of `ArraySpec`s.

<h3 id="close"><code>close</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
close()
```

Frees any resources used by the environment.

Implement this method for an environment backed by an external process.

This method be used directly

```python
env = Env(...)
# Use env.
env.close()
```

or via a context manager

```python
with Env(...) as env:
  # Use env.
```

<h3 id="current_time_step"><code>current_time_step</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
current_time_step()
```

Returns the current timestep.

<h3 id="observation_spec"><code>observation_spec</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
observation_spec()
```

Defines the observations provided by the environment.

May use a subclass of `ArraySpec` that specifies additional properties such
as min and max bounds on the values.

#### Returns:

An `ArraySpec`, or a nested dict, list or tuple of `ArraySpec`s.

<h3 id="render"><code>render</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
render(mode='rgb_array')
```

Renders the environment.

#### Args:

*   <b>`mode`</b>: One of ['rgb_array', 'human']. Renders to an numpy array, or
    brings up a window where the environment can be visualized.

#### Returns:

An ndarray of shape [width, height, 3] denoting an RGB image if mode is
`rgb_array`. Otherwise return nothing and render directly to a display
window.

#### Raises:

* <b>`NotImplementedError`</b>: If the environment does not support rendering.

<h3 id="reset"><code>reset</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
reset()
```

Starts a new sequence and returns the first `TimeStep` of this sequence.

Note: Subclasses cannot override this directly. Subclasses implement
_reset() which will be called by this method. The output of _reset() will
be cached and made available through current_time_step().

#### Returns:

A `TimeStep` namedtuple containing: step_type: A `StepType` of `FIRST`. reward:
0.0, indicating the reward. discount: 1.0, indicating the discount. observation:
A NumPy array, or a nested dict, list or tuple of arrays corresponding to
`observation_spec()`.

<h3 id="seed"><code>seed</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

```python
seed(seed)
```

Seeds the environment.

#### Args:

*   <b>`seed`</b>: Value to use as seed for the environment.

<h3 id="step"><code>step</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
step(action)
```

Updates the environment according to the action and returns a `TimeStep`.

If the environment returned a `TimeStep` with
<a href="../../../tf_agents/trajectories/time_step/StepType.md#LAST"><code>StepType.LAST</code></a>
at the previous step the implementation of `_step` in the environment should
call `reset` to start a new sequence and ignore `action`.

This method will start a new sequence if called after the environment has been
constructed and `reset` has not been called. In this case `action` will be
ignored.

Note: Subclasses cannot override this directly. Subclasses implement
_step() which will be called by this method. The output of _step() will be
cached and made available through current_time_step().

#### Args:

*   <b>`action`</b>: A NumPy array, or a nested dict, list or tuple of arrays
    corresponding to `action_spec()`.

#### Returns:

A `TimeStep` namedtuple containing: step_type: A `StepType` value. reward: A
NumPy array, reward value for this timestep. discount: A NumPy array, discount
in the range [0, 1]. observation: A NumPy array, or a nested dict, list or tuple
of arrays corresponding to `observation_spec()`.

<h3 id="time_step_spec"><code>time_step_spec</code></h3>

<a target="_blank" href="https://github.com/tensorflow/agents/tree/master/tf_agents/environments/py_environment.py">View
source</a>

``` python
time_step_spec()
```

Describes the `TimeStep` fields returned by `step()`.

Override this method to define an environment that uses non-standard values
for any of the items returned by `step()`. For example, an environment with
array-valued rewards.

#### Returns:

A `TimeStep` namedtuple containing (possibly nested) `ArraySpec`s defining
the step_type, reward, discount, and observation structure.
