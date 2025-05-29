v1.1 CVR Tuned Eye & Face Tracking Animator, as made by DragonSkyRunner

This package is intended to be used as a largely drop-in solution for a face tracking animator set up for a ChilloutVR avatar running through VRCFT. This does presume you have some amount of knowledge on how to edit Unity Animators, so if you know nothing about such things, grab a friend who can help.

As of the writing of this readme, this will necessitate the "OSC" mod by Kafeijao to have VRCFT's OSC messages get into the animator, and VRCFT itself configured for your face tracking hardware of choice. This is not a tutorial for that side of things.


Things to note:

This will use up 50/100 synced floats and 2 synced bools to work, out of what's available on a CVR avatar. For most avatars that should be well within the limits.

The eye gaze direction (ie, how much the eyes rotate around), due to the nature of how every avatar is typically wildly different in that regard, likely will require tuning of how far the eyes rotate. Ie: The animations for how far to rotate the eyes will have to be edited to move the eyes less/more.

This also presumes a couple of things about the avatar to truly be (largely) drop-in:
- The main avatar mesh the face tracking shapes are on is called "Body".
- The naming convention the face shapes follow is consistent with how most avatars name their face shapes after the introduction of Unified Expressions (Ie, "BrowDownLeft", "JawOpen", "MouthUpperLeft" etc.) (Virtually all Unified Expressions face tracking DLC do follow this naming schema.)

The set up by nature is meant to be 'simple' in terms of how it functions. Ie, no parameter smoothing or Binary Parameters or any such thing. The latter is unnecessary with the amount of parameter space CVR has for avatars, and the former is better suited for either being done as a mod (Which BTKSAUtils as made by DDAkebono facilitates), or a eventual native option.

Don't be afraid to tweak things in the layers for your avatar, when using this myself there is never a time where I don't end up tweaking things per-avatar, as every avatar has their own particulars with what makes sense for a given avatar.

Even if a avatar has Unified Expression shapes and follows the 'standard' naming convention, there is a chance that avatar is missing shapes that the animations are expecting due to a particular set of simplifications or only has a specific chunk of shapes (Using MouthCornerPullLeft/Right & MouthCornerSlantLeft/Right instead of using MouthSmileLeft/Right), so manual configuring of animations may still be necessary.

Install instructions:

- Import .unitypackage into project

- Copy over contents of the "Face Tracking Layers" Animator into the Animator you use for your avatar (You can box-select the contents of a Animator Layer, CTRC-C, and CTRL-V into a new layer in the target Animator.)

- Add in two bools into your Animator, named "EyeTracking" and "FaceTracking" as Bools don't copy over with copy/pasting Animator Layer contents.

- Make sure the following float parameters are not left at 0:
  - #Direct = 1
  - LeftEyeLidExpandedSqueeze = 0.8
  - RightEyeLidExpandedSqueeze = 0.8
  - EyesDilation = .5

- If we want to permanently have the eyes eye-tracking only, rename the existing eye bones "EyeTracking.L" and "EyeTracking.R" and make sure those bones are NOT set in the Unity Humanoid configurator.

- Making the eye gaze direction togglable is a bit more effort.  
  - In Blender, duplicate the eye bones in place and name them something memorable.
  - Back in Unity, add in two empties where the eye bones are, named "EyeTracking.L" and "EyeTracking.R".
  - Make sure the the eye bones the Unity Humanoid use are the ones that aren't weighted to anything we just made.
  - Attach the eye bones to both the empties and the unweighted Unity Humanoid eye bones with rotation constraints (as in with 2 sources), with the Unity Humanoid bones in the top slot, and the EyeTracking.L/.R in the bottom slot.

- Set up the "Eye Tracking" and "Face Tracking" toggles in the CVR Animator Component's Advanced Avatar Settings to be able to toggle things On/Off in-game.

- Assuming we have everything set up correctly, after tuning the eye gaze direction if necessary, you should be good to go!
