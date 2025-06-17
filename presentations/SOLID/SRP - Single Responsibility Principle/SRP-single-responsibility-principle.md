## Single Responsibility Principle
### The "S" in SOLID

---

### What is the "SRP"?

<img style="width: 300px; float: left; margin-top: 10px" src="https://upload.wikimedia.org/wikipedia/commons/2/27/Robert_C._Martin_surrounded_by_computers.jpg">

_"A class should have only one reason to change."_  
— Robert C. Martin

--

### And what does that mean?

- One sort of job per class 📋  <!-- .element: class="fragment" data-fragment-index="0" -->
- Do one thing and do it well ✨ <!-- .element: class="fragment" data-fragment-index="1" -->
- High cohesion, low responsibility scope 🧬 <!-- .element: class="fragment" data-fragment-index="2" -->
- Minimal coupling 🔗 <!-- .element: class="fragment" data-fragment-index="3" -->
- Separation of concerns (SoC) 🧩 <!-- .element: class="fragment" data-fragment-index="4" -->

---

### Real-World Example:
#### Store employee(s) 🏪

--

❌ **Bad:** A Swiss Army Knife Employee
  - Collects money from customers
  - Also stocks shelves
  - Also handles customer complaints
  - Also cleans the store

--

✅ **Good:** Specialized Roles
  - **Cashier:** Only handles transactions
  - **Stocker:** Only manages inventory
  - **Customer Service:** Only handles complaints
  - **Janitor:** Only maintains cleanliness

---

### Code Example:
#### A DocumentService 📃

--

### ❌ Bad

```javascript
class DocumentService {

  getDocument(id): Observable<Document> {
    return this.http.get<DocumentDto>(`/documents/${id}`)
      .pipe(
        map((d: DocumentDto) => this.mapToDocument(d))
      );
  }

  secureDocument(doc: Document): Observable<void> {
    doc.secure = true;
    const dto = this.mapToDocumentDto(doc);
    return this.http.put<void>(`/documents/${id}`, dto);
  }
}
```

--

**Problem:** Too many responsibilities! 😵
- Communicates with API
- Handles & manipulates functional data
- Translates between representations

⚡ It mixes concerns of technical and functional level!

--

### ✅ Better 

Handle & manipulate functional data:

```javascript
class DocumentService {
  getDocument(id): Observable<Document> {
    return this.documentClient.getDocument(id)
      .pipe(
        map((d: DocumentDto) => this.documentMapper.fromDto(d))
      );
  }

  secureDocument(doc: Document): Observable<void> {
    doc.secure = true;
    const dto = this.documentMapper.toDto(doc);
    return this.documentClient.updateDocument(dto);
  }
}
```

--

Communicate with API:

```javascript
class DocumentClient {

  getDocument(id): Observable<DocumentDto> {
    return this.http.get<DocumentDto>(`/documents/${id}`);
  }

  updateDocument(dto: DocumentDto): Observable<void> {
    return this.http.put<void>(`/documents/${id}`, dto)
  }
}
```

--

Translate between representations:

```javascript
class DocumentMapper {
  fromDto(dto: DocumentDto): Document { /* ... */ }
  toDto(doc: Document): DocumentDto { /* ... */ }
}
```

---

### Benefits of SRP 🎉

- **Easier to understand** 🧠
- **Easier to test** 🧪
- **Easier to maintain** 🔧
- **Reduced coupling** 🔗
- **Better reusability** ♻️
- **Cleaner architecture** 🏗️

---

### Basic tips 💡

Ask yourself ...

- ... What is the exact scope of my class, module, component? <!-- .element: class="fragment" data-fragment-index="0" -->
  <!-- Should be possible to precisely describe in one short name!; Coherence -> no free radicals! -->
- ... What does my class depend on? How much does it do? <!-- .element: class="fragment" data-fragment-index="1" -->
  <!-- Big numbers (imports, lines) are usually a bad indicator, Multiple import statements for unrelated **libraries** -->
- ... What are the in- and outputs? <!-- .element: class="fragment" data-fragment-index="2" -->
  <!-- A big variety often tells a lot already -->

--

## Common Anti-Patterns to Avoid ⚠️

- God Classes - Classes that do everything <!-- .element: class="fragment" data-fragment-index="0" -->
- Utility Classes - Catch-all static method containers <!-- .element: class="fragment" data-fragment-index="1" -->
- Manager Classes - Vague responsibilities <!-- .element: class="fragment" data-fragment-index="2" -->
- Mixed Concerns - UI logic mixed with business logic <!-- .element: class="fragment" data-fragment-index="3" -->

---

## Final Thoughts

<img style="float: right; width: 300px" src="https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fi%2Fxikbg4cgydydtn3zzf1r.png">

_"Treat your code as if it was a well-sorted kitchen drawer"_ 😉
