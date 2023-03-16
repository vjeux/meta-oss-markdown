# meta-oss-markdown
All the markdown files from the top 150 Meta Open Source repositories

LLMs are all the rage and one exciting use case is to use them within companies to make day to day activities more efficient. The challenge is that this data has very high confidentiality requirements and sending it to external parties is not advised. In order to help push forward getting LLMs for work a reality, I created this dataset.

This is a dataset of 8377 markdown files from Meta's top 159 open source projects sorted by stars. While not exactly representative to internal documentation, it should be close enough to be useful to play with models that can later be applied for internal use cases.

## How was the data collected?

I went to our internal tool that lists all the open source projects and scrolled for a while until it loaded 150 projects. In the dev tools I wrote:
```javascript
copy($$('.x2lwn1j.xeuugli.x78zum5.x1q0g3np').filter(e => e.innerText.match(/^[a-zA-Z0-9]+\n\/\n[a-zA-Z0-9]+$/)).map(e => 'git clone https://github.com/' + e.innerText.replace(/\n/g, '') + '.git').join('\n'))
```

which outputted:

```sh
git clone https://github.com/facebook/react.git
git clone https://github.com/facebook/docusaurus.git
git clone https://github.com/facebook/jest.git
git clone https://github.com/facebookresearch/Detectron.git
git clone https://github.com/facebook/folly.git
# ...
```

I added three more where the docs are not in the main repo:

```sh
git clone https://github.com/reactjs/reactjs.org.git
git clone https://github.com/hhvm/user-documentation
git clone https://github.com/facebook/react-native-website.git
```

I ran all those commands, it took a few hours to download all the repos.

I asked GPT-4 to figure out how to copy over all the markdown files keeping the file structure. This is insane that it actually did it and worked out of the box!!

<img width="363" alt="image" src="https://user-images.githubusercontent.com/197597/225683331-02e59409-44bf-41b5-8b1e-af79e51997ff.png">

And finally asked GPT-4 to tell me how to create a tarball.

<img width="362" alt="image" src="https://user-images.githubusercontent.com/197597/225683631-16dcdc31-d691-4fde-920b-ce3583c35099.png">
