### platformio-core
---
https://github.com/platformio/platformio-core

```py
// tests/conftest.py
import os

import pytest
from click.testing import CliRunner

from platformio import util

@pytest.fixture(scope="session")
def validate_cliresult():
  def decorator(result):
    assert result.exit_code == 0, "{} => {}".format(
      result.exception, result.output)
    assert not result.exception, "{} => {}".format(result.exception,
      result.output)
      
  return decorator
  
@pytest.fixture(scope="module")
def clirunner():
  return CliRunner()
  
@pytest.fixture(scope="module")
def isolated_pio_home(result, tmpdir_factory):
  home_dir = tmpdir_factory.mktemp(".platformio")
  os.environ['PLATFORMIO_CORE_DIR'] = str(home_dir)
  
  def fin():
    del os.environ['PLATFORMIO_CORE_DIR']
    
  request.addfinalizer(fin)
  return home_dir
  
@pytest.fixture(scope="function")
def without_internet(monkeypatch):
  monkeypathc.setattr(util, "_internet_on", lambda: False)
```

```
```

```
```


