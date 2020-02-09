# XS7 REPL on ESP8266EX

Build with Moddable and use `screen` to connect to REPL:

```
mcconfig -m -p esp

screen /dev/ttyUSB0 921600
```

```javascript
//replcore.js

		REPL.write(newline);
		if (this.incoming) {
			this.history.push(this.incoming);
			while (this.history.length > 20)
				this.history.shift();

			try {
				let result = REPL.eval(this.incoming);
				if (undefined === result)
					REPL.write("undefined", newline);
				else if (null === result)
					REPL.write("null", newline);
				else
					REPL.write(result.toString(), newline);
			}
			catch (e) {
				REPL.write(e.toString(), newline);
			}
		}
		this.prompt();
```

```c
void xs_repl_eval(txMachine* the)
{
	txStringStream aStream;

	aStream.slot = mxArgv(0);
	aStream.offset = 0;
	aStream.size = c_strlen(fxToString(the, mxArgv(0)));
	fxRunScript(the, fxParseScript(the, &aStream, fxStringGetter, mxProgramFlag), &mxGlobal, C_NULL, mxClosures.value.reference, C_NULL, C_NULL);
	mxPullSlot(mxResult);
}


```

## Issue 307

1. rename `$MODDABLE-SDK/xs/sources` to `$MODDABLE-SDK/xs/sources_new`

2. move `sources_old` in this folder to `$MODDABLE-SDK/xs/sources` 

   https://github.com/eco747/foton/search?q=mxClosures&unscoped_q=mxClosures

   https://github.com/Moddable-OpenSource/moddable/issues/307

## Moddable SDK

#### About

https://www.moddable.com/XS7-TC-39

[https://github.com/Moddable-OpenSource/moddable/blob/public/documentation/xs/XS%20Conformance.md](https://github.com/Moddable-OpenSource/moddable/blob/public/documentation/xs/XS Conformance.md)

[https://github.com/Moddable-OpenSource/moddable/blob/public/documentation/xs/XS%20in%20C.md](https://github.com/Moddable-OpenSource/moddable/blob/public/documentation/xs/XS in C.md)

#### Install 

[https://github.com/Moddable-OpenSource/moddable/blob/public/documentation/Moddable%20SDK%20-%20Getting%20Started.md#host-linux](https://github.com/Moddable-OpenSource/moddable/blob/public/documentation/Moddable SDK - Getting Started.md#host-linux)

[https://github.com/Moddable-OpenSource/moddable/blob/public/documentation/Moddable%20SDK%20-%20Getting%20Started.md#esp8266-linux](

## Data Sheets

https://www.espressif.com/sites/default/files/documentation/esp8266_reset_causes_and_common_fatal_exception_causes_en.pdf

https://www.espressif.com/sites/default/files/documentation/0a-esp8266ex_datasheet_en.pdf

# 