# UI Code for summarizing PDF
This is a UI code for a simple application to summarize content of a PDF file. Below diagram shows interaction between different components of this application:
![PDF File Sequence Diagram](PDF-Summary.svg)

The UI code to allow uploading the file and POSTing it to the service is shown below:  
```
    <form className="mt-6" onSubmit={onSubmit}>
      <div class="mb-6">
        <input
          type="file"
          name="file"
          onChange={(e) => setFile(e.target.files?.[0])}
        />
      </div>
    </form>

  const onSubmit = async (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault()
    if (!file) return
    setIsLoading(true);
    try {
      const data = new FormData()
      data.set('file', file)

      const res = await fetch(serviceUrl, {
        method: 'POST',
        body: data
      })
      // handle the error
      if (!res.ok) throw new Error(await res.text())
      setIsLoading(false);
      const resJ = await res.json();
      setSummary(resJ.completion);
    } catch (e: any) {
      // Handle errors here
      console.error(e)
      setIsLoading(false);
    }
  }
```

The code for the service layer is available here. [https://github.com/sekharkafle/pdflambda](https://github.com/sekharkafle/pdflambda)

Screenshot of the fully functional app:
![PDF UI](/assets/pdf-summary.png)

Happy Summarizing!!!
