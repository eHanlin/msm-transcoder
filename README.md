msm-transcoder
=================

## Install

```
python setup.py install
```

## Usage

Decode binary from ascii list.

```

buffers = map( ord, session_str )
data = transcoder.deserialize( buffers )

```

Encode dict into ascii list.

```

data["principalData"]["pythonttest"] = "123344"
transcoder.serialize( data )

```

## Example

```

import base64
import pylibmc
from msm_transcoder import Transcoder

mc = pylibmc.Client(["127.0.0.1"],  binary=True)

session_str = base64.b64decode( session )
buffers = map( ord, session_str )

transcoder = Transcoder()
data = transcoder.deserialize( buffers )

data["principalData"]["pythonttest"] = "123344"

output = base64.b64encode( ''.join( map( chr, transcoder.serialize( data ) ) ) )
mc.set( sessionId , output)

```

