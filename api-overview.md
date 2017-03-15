# VS Code SCM API Overview

This page is where we will build up the documentaiton for that will end up on our website for SCM Provider creators.  It will be much like the docs for [language extensions](http://code.visualstudio.com/docs/extensions/language-support) and [debuggers](http://code.visualstudio.com/docs/extensionAPI/api-debugging).

However, right now it's a work in progress :)

## Relevant Preview APIs

```TypeScript
declare module 'vscode' {

	/**
	 * Defines a generalized way of reporing progress updates.
	 */
	export interface Progress<T> {

		/**
		 * Report a progress update.
		 * @param value A progress item, like a message or an updated percentage value
		 */
		report(value: T): void
	}

	export namespace window {

		/**
		 * Show window-wide progress, e.g. in the status bar, for the provided task. The task is
		 * considering running as long as the promise it returned isn't resolved or rejected.
		 *
		 * @param task A function callback that represents a long running operation.
		 */
		export function withWindowProgress<R>(title: string, task: (progress: Progress<string>, token: CancellationToken) => Thenable<R>): Thenable<R>;

		export function withScmProgress<R>(task: (progress: Progress<number>) => Thenable<R>): Thenable<R>;

		export function sampleFunction(): Thenable<any>;
	}

	export interface SCMResourceThemableDecorations {
		readonly iconPath?: string | Uri;
	}

	export interface SCMResourceDecorations extends SCMResourceThemableDecorations {
		readonly strikeThrough?: boolean;
		readonly light?: SCMResourceThemableDecorations;
		readonly dark?: SCMResourceThemableDecorations;
	}

	export interface SCMResource {
		readonly uri: Uri;
		readonly decorations?: SCMResourceDecorations;
	}

	export interface SCMResourceGroup {
		readonly id: string;
		readonly label: string;
		readonly resources: SCMResource[];
	}

	export interface SCMProvider {
		readonly label: string;
		readonly resources: SCMResourceGroup[];
		readonly onDidChange: Event<SCMResourceGroup[]>;
		readonly count?: number | undefined;
		readonly state?: string;

		getOriginalResource?(uri: Uri, token: CancellationToken): ProviderResult<Uri>;
		open?(resource: SCMResource, token: CancellationToken): ProviderResult<void>;
		drag?(resource: SCMResource, resourceGroup: SCMResourceGroup, token: CancellationToken): ProviderResult<void>;
		acceptChanges?(token: CancellationToken): ProviderResult<void>;
	}

	export interface SCMInputBox {
		value: string;
		readonly onDidChange: Event<string>;
	}

	export namespace scm {
		export const onDidChangeActiveProvider: Event<SCMProvider>;
		export let activeProvider: SCMProvider | undefined;
		export const inputBox: SCMInputBox;

		export function getResourceFromURI(uri: Uri): SCMResource | SCMResourceGroup | undefined;
		export function registerSCMProvider(id: string, provider: SCMProvider): Disposable;
	}

	export interface LineChange {
		readonly originalStartLineNumber: number;
		readonly originalEndLineNumber: number;
		readonly modifiedStartLineNumber: number;
		readonly modifiedEndLineNumber: number;
	}

	export function computeDiff(oneDocument: TextDocument, otherDocument: TextDocument): Thenable<LineChange[]>;
}
```


