Goal: Audio to Audio in command line

Then into code as a possible API


Audio to Audio

Detect transients - drums (kick & snare)
Riffusion bass without transients - instruments
Separate drums from the rest
Boost transients all the way and add white noise to them (snare may need some tail or decay)
Or replace transients with real drum samples
Possibly arrange segments of instruments

Make sure for instruments to add distortion to it for dnb/dubstep/808 bass sounds
Can make instruments part of the sample generation algorithm
Can add chopped non transients instruments and put them into the pattern loop generator

Can be similar to dance diffusion


Try this for streamlit deployment:
It sounds like you have a local package called riffusion that includes a subpackage streamlit with a file playground.py. When you deploy the app, the package riffusion is not being found by the deployment environment.

One way to fix this is to make sure that the riffusion package is installed in the deployment environment. You can do this by creating a setup.py file in the root of your project with the following content:

python
Copy code
from setuptools import setup, find_packages

setup(
    name='riffusion',
    version='0.1',
    packages=find_packages(),
    install_requires=[
        'streamlit',
        # add any other dependencies here
    ],
)
This setup.py file specifies that the riffusion package should be installed along with any other dependencies required by your app, such as streamlit. You can then deploy your app by running python setup.py install in the deployment environment.

Alternatively, you can try modifying your imports in playground.py to use relative imports. For example, if you have a module in the streamlit subpackage that needs to import from riffusion.datatypes, you can use the following import statement:

python
Copy code
from ..datatypes import InferenceInput, PromptInput
This will import the InferenceInput and PromptInput classes from the datatypes module in the parent riffusion package. However, note that relative imports can be fragile and may not work correctly in all situations.