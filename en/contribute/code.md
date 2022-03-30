# Source Code Management

## Branching Model

The PX4 project uses a three-branch Git branching model:

* [master](https://github.com/PX4/PX4-Autopilot/tree/master) is by default unstable and sees rapid development.
* [beta](https://github.com/PX4/PX4-Autopilot/tree/beta) has been thoroughly tested. It's intended for flight testers.
* [stable](https://github.com/PX4/PX4-Autopilot/tree/stable) points to the last release.

We try to retain a [linear history through rebases](https://www.atlassian.com/git/tutorials/rewriting-history) and avoid the [Github flow](https://guides.github.com/introduction/flow/). 
However, due to the global team and fast moving development we might resort to merges at times.

To contribute new functionality, [sign up for Github](https://help.github.com/articles/signing-up-for-a-new-github-account/), then [fork](https://help.github.com/articles/fork-a-repo/) the repository, [create a new branch](https://help.github.com/articles/creating-and-deleting-branches-within-your-repository/), add your changes, and finally [send a pull request](https://help.github.com/articles/using-pull-requests/). 
Changes will be merged when they pass our [continuous integration](https://en.wikipedia.org/wiki/Continuous_integration) tests.

All code contributions have to be under the permissive [BSD 3-clause license](https://opensource.org/licenses/BSD-3-Clause) and all code must not impose any further constraints on the use.

## Code Style

PX4 uses the [Google C++ style guide](https://google.github.io/styleguide/cppguide.html), with the following modifications:

### Tabs

We will use tabs (equivalent to 4 spaces).

### Line Length

Our maximum line length is 120 characters.

### File Extensions

- Header files should use the .hpp extension and implementation files should use the .cpp extension. This allows tools to determine the content of files, C++ or C.

- [PLACEHOLDER] Test file naming?

- One exception to the rules above are the MAVLink streams in [src/modules/mavlink/streams](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/mavlink/streams) which are ALL_UPPERCASE.hpp matching the MAVLink message name.

### Function and Method Names

We will use `lowerCamelCase()` for functions and methods to *visually* distinguish them from `ClassConstructors()` and `ClassNames`.

### Class Privacy Keywords

Use *zero* spaces before `public:`, `private:`, or `protected:`.

### Example Code Snippet

```
class MyClass {
public:

    /**
     * Brief description of what this function does.
     *
     * @param[in] input_param Clear description of the input [units]
     * @return Whatever we are returning [units]
     */
    float doSomething(const float input_param) const {
        const float in_scope_variable = input_param + kConstantFloat;
        return in_scope_variable * private_member_variable_;
    }

    /**
     * Set the private member [units]
     */
    void setPrivateMember(const float private_member_variable) { private_member_variable_ = private_member_variable; }

    /**
     * @return Whatever we are "getting" [units]
     */
    float getPrivateMember() const { return private_member_variable_; }

private:
    
    // Clear meaning within context [units if not specified in name]
    static constexpr float kConstantFloat = ...;  

    // Clear description of the variable [units]
    float private_member_variable_{...};
};
```

## In-Source Documentation

PX4 developers are encouraged to create appropriate in-source documentation.

:::note
Source-code documentation standards are not enforced, and the code is currently inconsistently documented.
We'd like to do better!
:::
  
Currently we have two types of source-based documentation:
- `PRINT_MODULE_*` methods are used for both module run time usage instructions and for the [Modules & Commands Reference](../modules/modules_main.md) in this guide.
  - The API is documented [in the source code here](https://github.com/PX4/PX4-Autopilot/blob/v1.8.0/src/platforms/px4_module.h#L381). 
  - Good examples of usage include the [Application/Module Template](../modules/module_template.md) and the files linked from the modules reference.
* We encourage other in-source documentation *where it adds value/is not redundant*. 

  :::tip
  Developers should name C++ entities (classes, functions, variables etc.) such that their purpose can be inferred - reducing the need for explicit documentation.
  :::
  
  - Do not add documentation that can trivially be assumed from C++ entity names.
  - Commonly you may want to add information about corner cases and error handling.
  - [Doxgyen](http://www.doxygen.nl/) tags should be used if documentation is needed: `@class`, `@file`, `@param`, `@return`, `@brief`, `@var`, `@see`, `@note`. A good example of usage is [src/modules/events/send_event.h](https://github.com/PX4/PX4-Autopilot/blob/master/src/modules/events/send_event.h).

## Commits and Commit Messages

Please use descriptive, multi-paragraph commit messages for all non-trivial changes. Structure them well so they make sense in the one-line summary but also provide full detail.

```
Component: Explain the change in one sentence. Fixes #1234

Prepend the software component to the start of the summary
line, either by the module name or a description of it.
(e.g. "mc_att_ctrl" or "multicopter attitude controller").

If the issue number is appended as <Fixes #1234>, Github
will automatically close the issue when the commit is
merged to the master branch.

The body of the message can contain several paragraphs.
Describe in detail what you changed. Link issues and flight
logs either related to this fix or to the testing results
of this commit.

Describe the change and why you changed it, avoid to
paraphrase the code change (Good: "Adds an additional
safety check for vehicles with low quality GPS reception".
Bad: "Add gps_reception_check() function").

Reported-by: Name <email@px4.io>
```

**Use **`git commit -s`** to sign off on all of your commits.** This will add `signed-off-by:` with your name and email as the last line.

This commit guide is based on best practices for the Linux Kernel and other [projects maintained](https://github.com/torvalds/subsurface/blob/a48494d2fbed58c751e9b7e8fbff88582f9b2d02/README#L88-L115) by Linus Torvalds.
