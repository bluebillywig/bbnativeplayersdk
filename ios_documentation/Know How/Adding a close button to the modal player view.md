# Adding a close button to the modal player view

Use the player api to:

- get a reference to the ModalPlayerView (UIView)
- call the method closeModalPlayer() to close the Modal View

Below is a piece of example Swift code for how to add close a button to the modal player view. 

    self.bbPlayerView = BBNativePlayer.createModalPlayerView(uiViewController: self, jsonUrl: "https://bb.dev.bbvms.com/p/default/c/1092747.json", options: ["autoPlay": false])
    bbPlayerView!.delegate = self

    if let modalPlayerView = bbPlayerView?.player.getModalPlayerView() {
        //Create UIButton
        let modalCloseButton = UIButton(type: .system)
        modalCloseButton.backgroundColor = .red
        modalCloseButton.setTitle("close", for: .normal)

        modalPlayerView.addSubview(modalCloseButton)
        modalCloseButton.translatesAutoresizingMaskIntoConstraints = false
        modalCloseButton.centerXAnchor.constraint(equalTo: modalPlayerView.safeAreaLayoutGuide.centerXAnchor).isActive = true
        modalCloseButton.topAnchor.constraint(equalTo: modalPlayerView.safeAreaLayoutGuide.topAnchor ).isActive = true
        modalCloseButton.heightAnchor.constraint(equalToConstant: 40).isActive = true
        modalCloseButton.widthAnchor.constraint(equalToConstant: 60) .isActive = true

        // Set button action
        modalCloseButton.addTarget(self, action: #selector(closeModal(_:)), for: .touchUpInside)
    }

    @objc func closeModal(_ sender:UIButton!) {
        bbPlayerView?.player.closeModalPlayer()
    }
